# check-invoices

## 1. Sử dụng công thức Excel

```bash
=IF(B17="";"";
  LET(
      soHD; B17;
      dong; MATCH(soHD; 'sheet 1'!D:D; 0);
      IF(ISNA(dong); "Không Có Hợp Đồng!";
          LET(
              ngay_s1; INDEX('sheet 1'!E:E; dong);
              mst_s1; INDEX('sheet 1'!F:F; dong);
              ten_s1; INDEX('sheet 1'!G:G; dong);
              tien1_s1; INDEX('sheet 1'!H:H; dong);
              tien2_s1; INDEX('sheet 1'!I:I; dong);
              loi; TEXTJOIN(", "; TRUE;
                  IF(C17<>ngay_s1; "Sai Ngày"; "");
                  IF(D17<>ten_s1; "Sai Tên Người Bán"; "");
                  IF(E17<>mst_s1; "Sai MST"; "");
                  IF(F17<>tien1_s1; "Sai Tổng Tiền Chưa Thuế"; "");
                  IF(G17<>tien2_s1; "sai Tổng Tiền thuế"; "")
              );
              IF(loi=""; "Khớp"; loi)
          )
      )
  )
)
```

#### 1.1 Cách hoạt động của công thức:

- Kiểm tra xem ô **B17** (Số hóa đơn) có trống không, nếu trống thì bỏ qua.
- Dùng **MATCH** tìm vị trí dòng của Số hóa đơn (B17) bên Cột D của sheet 1. Nếu không tìm thấy, trả về "Không Có Hợp Đồng!".
- Nếu tìm thấy, dùng **INDEX** lấy toàn bộ thông tin đối ứng ở sheet 1.
- Lần lượt so sánh Ngày, Tên, MST, Tiền với sheet 2. Nếu sai lệch ở đâu, hàm **TEXTJOIN** sẽ nối các lỗi lại với nhau (VD: "Sai MST, Sai Tiền thuế"). Nếu không có lỗi nào, trả về "Khớp".

## 2. Sử dụng VBA được tích hợp sẵn trong excel

#### 2.1 Cách làm (Chỉ cần làm 1 lần):

- Mở cửa sổ VBA:
  - Mở file Excel của bạn lên.
  - Nhấn tổ hợp phím Alt + F11 trên bàn phím. (Một cửa sổ mới có tên là Microsoft Visual Basic for Applications sẽ hiện ra).
- Tạo nơi chứa code:
  - Trong cửa sổ mới, nhìn lên thanh Menu, chọn Insert -> Module.
  - Một cửa sổ trắng sẽ hiện ra bên phải.
- Dán đoạn code sau vào cửa sổ trắng đó:

  ```vba
  Sub KiemTraHoaDon()
    Dim ws1 As Worksheet, ws2 As Worksheet
    Dim lr1 As Long, lr2 As Long
    Dim i As Long
    Dim soHD As String, kq As String
    Dim fndRow As Range
    
    ' Định nghĩa 2 sheet
    Set ws1 = ThisWorkbook.Sheets("sheet 1")
    Set ws2 = ThisWorkbook.Sheets("sheet 2")
    
    ' Tìm dòng cuối cùng có dữ liệu
    lr1 = ws1.Cells(ws1.Rows.Count, "D").End(xlUp).Row
    lr2 = ws2.Cells(ws2.Rows.Count, "B").End(xlUp).Row
    
    ' Xóa dữ liệu cũ ở cột Kết quả sheet 2 (từ dòng 17 đến cuối)
    If lr2 >= 17 Then
        ws2.Range("I17:I" & lr2).ClearContents
    End If
    
    ' Bắt đầu chạy vòng lặp kiểm tra từ dòng 17 ở sheet 2
    For i = 17 To lr2
        soHD = ws2.Cells(i, 2).Value ' Cột B: Số hóa đơn
        kq = ""
        
        If soHD <> "" Then
            ' Tìm số hóa đơn bên sheet 1 cột D
            Set fndRow = ws1.Range("D7:D" & lr1).Find(What:=soHD, LookIn:=xlValues, LookAt:=xlWhole)
            
            If fndRow Is Nothing Then
                ws2.Cells(i, 9).Value = "Không Có Hợp Đồng!" ' Cột I: Kết quả
            Else
                ' So sánh dữ liệu
                Dim r As Long
                r = fndRow.Row
                
                ' So sánh Ngày (Cột C sheet 2 vs Cột E sheet 1)
                If ws2.Cells(i, 3).Value <> ws1.Cells(r, 5).Value Then kq = kq & "Sai Ngày, "
                ' So sánh Tên (Cột D sheet 2 vs Cột G sheet 1)
                If Trim(ws2.Cells(i, 4).Value) <> Trim(ws1.Cells(r, 7).Value) Then kq = kq & "Sai Tên Người Bán, "
                ' So sánh MST (Cột E sheet 2 vs Cột F sheet 1)
                If CStr(ws2.Cells(i, 5).Value) <> CStr(ws1.Cells(r, 6).Value) Then kq = kq & "Sai MST, "
                ' So sánh Tiền chưa thuế (Cột F sheet 2 vs Cột H sheet 1)
                If ws2.Cells(i, 6).Value <> ws1.Cells(r, 8).Value Then kq = kq & "Sai Tổng Tiền Chưa Thuế, "
                ' So sánh Tiền thuế (Cột G sheet 2 vs Cột I sheet 1)
                If ws2.Cells(i, 7).Value <> ws1.Cells(r, 9).Value Then kq = kq & "Sai Tổng Tiền Thuế, "
                
                ' Xuất kết quả
                If kq = "" Then
                    ws2.Cells(i, 9).Value = "Khớp"
                Else
                    ' Xóa dấu phẩy và khoảng trắng thừa ở cuối
                    ws2.Cells(i, 9).Value = Left(kq, Len(kq) - 2)
                End If
            End If
        End If
    Next i
    
    MsgBox "Đã Kiểm Tra Xong!", vbInformation, "Thông Báo"
  End Sub
  ```
- Lưu và đóng:
  - Tắt cửa sổ VBA (bấm dấu X góc phải trên cùng).
  - Bây giờ, file Excel của bạn phải được Lưu dưới dạng cho phép Macro (Save As -> Excel Macro-Enabled Workbook (*.xlsm)) để đoạn code này không bị mất đi.

#### 2.2 Cách sử dụng (Hàng tháng):
- Mỗi khi bạn có dữ liệu mới, bạn chỉ cần vào tab View -> chọn Macros -> chọn KiemTraHoaDon và bấm nút Run. Excel sẽ tự động chạy qua toàn bộ các dòng và điền kết quả vào Cột I (Kết quả) ở Sheet 2 trong nháy mắt.

## 3. Sử dụng với Google Sheets

#### 3.1 Hướng dẫn cách cài đặt và chạy trên Google Sheets
- Mở trình chỉnh sửa Script:
  - Trên file Google Sheets của bạn, bấm vào menu Tiện ích mở rộng (Extensions) -> Chọn Apps Script.
- Dán mã Code:
  - Xóa toàn bộ đoạn code mặc định đang có sẵn trong khung làm việc.
  - Copy toàn bộ đoạn code JavaScript dưới đây và dán vào đó.
    ```js
    function kiemTraHoaDon() {
      var ss = SpreadsheetApp.getActiveSpreadsheet();
      var ws1 = ss.getSheetByName("sheet 1");
      var ws2 = ss.getSheetByName("sheet 2");
    
      // Lấy toàn bộ dữ liệu 2 sheet
      var data1 = ws1.getDataRange().getValues();
      var data2 = ws2.getDataRange().getValues();
    
      // Tạo kho lưu trữ dữ liệu sheet 1 dựa trên "Số hóa đơn" (Cột D - chỉ số 3)
      var sheet1Map = {};
      for (var r = 6; r < data1.length; r++) { // Dòng 7 tương ứng chỉ số 6
        var soHD = String(data1[r][3]).trim();
        if (soHD !== "") {
          sheet1Map[soHD] = {
            ngay: data1[r][4],   // Cột E: Ngày lập
            mst: String(data1[r][5]).trim(),    // Cột F: MST
            ten: String(data1[r][6]).trim(),    // Cột G: Tên
            tien1: data1[r][7],  // Cột H: Chưa thuế
            tien2: data1[r][8]   // Cột I: Tiền thuế
          };
        }
      }
    
      var results = [];
    
      // Duyệt dữ liệu từ dòng 17 sheet 2 (chỉ số 16)
      for (var i = 16; i < data2.length; i++) {
        var soHD2 = String(data2[i][1]).trim(); // Cột B: Số hóa đơn
        if (soHD2 === "") {
          results.push([""]);
          continue;
        }
    
        if (!sheet1Map.hasOwnProperty(soHD2)) {
          results.push(["KHÔNG CÓ HĐ"]);
        } else {
          var match = sheet1Map[soHD2];
          var errors = [];
    
          // So sánh Ngày (Cột C)
          if (formatDate(data2[i][2]) !== formatDate(match.ngay)) {
            errors.push("sai Ngày");
          }
          // So sánh Tên (Cột D)
          if (String(data2[i][3]).trim() !== match.ten) {
            errors.push("SAI TÊN CTY");
          }
          // So sánh MST (Cột E)
          if (String(data2[i][4]).trim() !== match.mst) {
            errors.push("sai MST");
          }
          // So sánh Tiền chưa thuế (Cột F)
          if (Number(data2[i][5]) !== Number(match.tien1)) {
            errors.push("sai Tiền chưa thuế");
          }
          // So sánh Tiền thuế (Cột G)
          if (Number(data2[i][6]) !== Number(match.tien2)) {
            errors.push("sai Tiền thuế");
          }
    
          if (errors.length === 0) {
            results.push(["khớp"]);
          } else {
            results.push([errors.join(", ")]);
          }
        }
      }
    
      // Ghi kết quả vào Cột I (Cột số 9) bắt đầu từ dòng 17 ở Sheet 2
      if (results.length > 0) {
        ws2.getRange(17, 9, results.length, 1).setValues(results);
      }
    
      SpreadsheetApp.getUi().alert("Đã kiểm tra xong!");
    }
    
    // Hàm hỗ trợ định dạng ngày tháng để so sánh chính xác
    function formatDate(val) {
      if (!val) return "";
      if (val instanceof Date) {
        return Utilities.formatDate(val, Session.getScriptTimeZone(), "dd/MM/yyyy");
      }
      return String(val).trim();
    }
    ```
  - Bấm vào biểu tượng Lưu (Save / Hình đĩa mềm) hoặc nhấn Ctrl + S.
- Chạy thử lần đầu:
  - Bấm nút Chạy (Run) ở phía trên thanh công cụ.
  - Ở lần chạy đầu tiên, Google sẽ hiển thị thông báo "Yêu cầu quyền truy cập" (Authorization required) -> Bấm Xem lại quyền (Review Permissions) -> Chọn tài khoản Google của bạn -> Bấm Nâng cao (Advanced) -> Chọn Đi tới dự án (không an toàn) -> Bấm Cho phép (Allow).
- Kiểm tra kết quả:
  - Quay lại tab Google Sheets, bạn sẽ thấy cột I (Kết quả) từ dòng 17 ở Sheet 2 đã tự động được điền kết quả đối chiếu.
