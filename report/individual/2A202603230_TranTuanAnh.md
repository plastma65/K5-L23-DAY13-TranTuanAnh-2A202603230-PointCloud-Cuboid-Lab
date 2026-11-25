# Báo cáo Day 13 — Trần Tuấn Anh, 2A202603230

## 1. Kết luận trước
- **Mã số:** 2A202603230 · **Task:** `D13-2A202603230` (CVAT local, task #21)
- **10 frame:** s01f19, s01f40, s02f16, s02f31, s03f19, s03f53, s04f17, s04f45, s05f24, s05f48
- **Môi trường:** Windows 11, Chrome, CVAT server **2.74.1** (cvat-sdk 2.83.0 báo cảnh báo lệch phiên bản; tạo task, xuất bảng A, `preview`, `selfcheck` vẫn chạy được)
- **Bạn ngồi cạnh:** không có
- **Vòng hiệu chuẩn:** không tham gia, không tạo task chung `D13-HC485087`

Tổng cộng 90 cuboid trên 10 frame. Frame ít nhất là s05f48 (3 cuboid) vì không thể thấy rõ những cuboid ở quá xa hoặc các tia gần như không rõ đến mức có thể xác định được vật thể; s01f19 có 5 cuboid, dưới mức 8 của đề vì các vật thể sau mức 5 gần như không thể nhận diện vì các tia quá loãng. `selfcheck` cờ 0/90 cuboid. Tôi tin nhất phần kích thước vì tất cả đều không nằm ngoài phạm vi từ guideline; phần còn yếu nhất là xác định phạm vi giữ xe và mặt đất vì đa số các trường hợp là vì xe quá cao hay xe quá thấp so với mặt đất.


## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s01f19 | phía trước xe là -y nhìn từ trên xuống ;+x chỉ về phía bên trái xe và +y chỉ về phía đuôi xe | mặt đường phẳng | vật xa nhất đọc được tầm 70-80m | loại vật có thể thấy là xe `car` | vật phía sau là xe `car` | cụm chưa đọc được là người `pedestrian` |
| s01f40 | phía trước xe là -y nhìn từ trên xuống ;+x chỉ về phía bên trái xe có thể thấy được đầu xe kế bên và +y chỉ về phía đuôi xe | mặt đường phẳng | vật xa nhất đọc được tầm 60m | loại vật có thể thấy là xe `car` | vật phía sau là xe `car` | cụm chưa đọc được là xe `car` nằm ngoài phạm vi tia có thể chiếu tới |

3 điều **chỉ camera** cho biết và 3 điều **chỉ LiDAR** cho biết, lấy từ chính hai frame trên.

- Camera thu nhận màu sắc và ánh sáng thực tế.
- Camera đọc chữ viết, ký hiệu và dải phân cách chia 2 làn, cột đèn xanh đèn đỏ.
- Camera có thể nhận diện chi tiết vật thể như xe `car`, xe `bus`, xe `truck`.
- LiDAR có thể cho biết khoảng cách từ tia chiếu tới các xe `car` phía trước.
- LiDAR có thể cho biết khoảng cách từ xe phía trước trong khi vẫn giữ ở tốc độ nhất định.
- LiDAR có khả năng nhận các vật thể trong bán kính 360 độ xung quanh từ các tia chiếu tới và trở lại. 

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
|---|---|---|
| `s02f16`;`s02f31` | phía trước nằm ở cạnh -y nhìn từ trên xuống | không có |
| `s03f19`;`s03f53` | phía trước nằm ở cạnh -y nhìn từ trên xuống | không có |
| `s04f17`;`s04f45` | phía trước nằm ở cạnh -y nhìn từ trên xuống | không có |
| `s05f24`;`s05f48` | phía trước nằm ở cạnh -y nhìn từ trên xuống | không có |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | `s01f19`, `id 1` | `car` | Mũi tên đúng hướng | Đáy đã chạm đường | Đã kiểm cả Top/Side/Front | kích thước đã chuẩn theo bảng 4.3 thuộc file `docs/GUIDELINE.md` |
| (b) xe buýt hoặc xe tải | `s01f19`,`id 2` | `bus` | mũi tên đúng hướng | Đáy đã chạm đường | Đã kiểm cả Top/Side/Front | kích thước đã chuẩn theo bảng 4.3 thuộc file `docs/GUIDELINE.md` |
| (c) người đi bộ hoặc xe hai bánh | `s05f24`, `id 11` | `Cyclist` | mũi tên đúng hướng | Đáy đã chạm đường | Đã kiểm cả Top/Side/Front | kích thước đã chuẩn theo bảng 4.3 thuộc file `docs/GUIDELINE.md`

**Vòng hiệu chuẩn:** tôi không tham gia vòng hiệu chuẩn (không tạo và không vẽ trên task chung `D13-HC485087`), nên không có số liệu so lệch với các bạn.

Vật bỏ qua vì không đủ cơ sở:
- `s01f19`, phía sau, khoảng 80 m: nghi là một xe con (Car). Loại nghi vấn: LOW_VISIBILITY, UNCERTAIN_SCOPE (ngoài phạm vi 50 m của lab). Lý do: chỉ thấy vài chấm giống đầu xe, không chắc có đúng là xe không, nên tôi không vẽ.

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | `s05f24` / `t4-1-bong-che.png` / frame của tôi | Giả thuyết: thân xe thu dữ liệu hoặc vật ở rất gần LiDAR phía sau chặn tia, tạo vùng mù | Phía sau xe thu dữ liệu có một vùng trống điểm hình quạt, kéo tới trước xe con #81 (số đối tượng trong danh sách CVAT) | Vùng trống sau vật che là chưa quan sát được, không phải đường trống: không vẽ cuboid cho vật không có điểm. Vật bị che một phần (như xe con #81 nếu mất một phần điểm) thì bật occluded và cuboid bao phần suy ra được |
| 2. Thưa ở xa | `s05f24` / `t4-2-thua-o-xa.png` / frame của tôi | Giả thuyết: các tia LiDAR toả ra theo góc nên càng xa điểm càng thưa; xe con #77 phía trước cũng có thể chặn một phần tia | Phía sau xe con #77 (số đối tượng trong danh sách CVAT) có một vùng lớn hình chữ nhật rất thưa điểm | Vật nằm trong vùng thưa: thấy được khoảng 15–20% thể tích thì vẽ; ít hơn thì bỏ qua và ghi LOW_VISIBILITY |
| 3. Phản xạ thấp / ít điểm bất thường | `s02f16` / `t4-3-phan-xa-thap.png` / frame của tôi | Giả thuyết: xe nằm gần như song song với trục x của xe thu dữ liệu nên tia chiếu xiên vào thân xe, ít tia phản xạ về; các xe làn ngược chiều đứng thẳng hàng cách nhau khoảng 2–3 m còn che bớt nhau | Xe con #16 (số đối tượng trong danh sách CVAT) ở làn ngược chiều có rất ít điểm so với kích thước xe | Chỉ ghi giả thuyết, không khẳng định nguyên nhân. Vẽ khi đủ cơ sở (thấy khoảng 15–20% thể tích hoặc ảnh camera rõ); không thì bỏ qua và ghi LOW_VISIBILITY |
| 4. Điểm lạ | `s05f24` / `t4-4-diem-la.png` / frame của tôi | Giả thuyết: dải phân cách và các cọc giao thông hai bên đường là vật mảnh, cao cỡ người, nên cụm điểm của chúng có hình dáng giống người đi bộ hoặc xe hai bánh | Ở hai bên đường có những cụm điểm đứng thẳng, nhìn giống Pedestrian hoặc Cyclist; đối chiếu với vị trí dải phân cách và cọc giao thông thì đó là vật cố định bên đường | Không gán điểm lạ thành vật: không vẽ cuboid Pedestrian hay Cyclist cho các cụm này. Đối chiếu ảnh camera; nếu vẫn không chắc thì ghi UNCERTAIN_CLASS vào báo cáo |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-<MÃ SỐ>-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| s05f24, 8, Car | −0,865 m | 1,591 m | −1,660 m | 13,36 m | 13,39 m | 270,2° | Chạm đường (lệch 0,04 m so với −1,7 m) |
| s02f16, 5, Car | −1,199 m | 1,608 m | −2,003 m | 4,57 m | 4,72 m | 90,1° | lệch 0,30 m so với −1,7 m, chìm |
| s02f31, 6, Car | −1,008 m | 1,588 m | −1,802 m | 18,87 m | 18,90 m | 263,3° | Chạm đường (lệch 0,10 m so với −1,7 m) |

(a) **Gần nhất:** s01f40, idx 1, Car: `dist_m` = 3,14 m, r = 3,31 m. **Xa nhất (trong 50 m):** s02f31, idx 5, Car: `dist_m` = 48,00 m, r = 48,02 m.

(b) **Kích thước so với bảng 4.3:**
- Người đi bộ s03f19, idx 16: l = 0,524 m, w = 0,610 m, h = 1,947 m. Bảng 4.3 (người lớn): 0,4–0,9 × 0,5–0,9 × 1,50–1,95 m, nên cả ba chiều nằm trong khoảng; riêng h sát cận trên.
- Xe con s03f53, idx 3: l = 4,797 m, w = 2,043 m, h = 1,593 m. So với sedan/hatchback (3,8–5,0 × 1,70–1,90 × 1,40–1,60 m): l và h trong khoảng, w lớn hơn 1,90 m. So với SUV/minivan (4,4–5,3 × 1,80–2,10 × 1,65–2,10 m): l và w trong khoảng, h thấp hơn 1,65 m.

xe này là sedan vì box gồm cả kính chiếu hậu nên rộng hơn một chút.

(c) **Yaw:** xe cùng chiều phía trước s04f17, idx 5: `yaw_deg` = 271,0°, gần 270°. Xe ngược chiều s05f24, idx 6: `yaw_deg` = 89,4°, gần 90°. Cả hai đúng hướng.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| s05f48, 1, Car | 4,66 m | 9632 |
| s02f31, 4, Car | 14,70 m | 739 |
| s02f31, 8, Car | 23,90 m | 244 |
| s03f19, 18, Car | 33,23 m | 200 |

**Quy luật:** khi `dist_m` tăng từ khoảng 4,66 m lên 14,70 m (xa gấp khoảng 3,2 lần) thì số điểm giảm từ 9632 còn 739 (còn khoảng 7,7%); từ 14,70 m lên 33,23 m (xa gấp khoảng 2,3 lần) thì số điểm còn 200 (khoảng 27%). Số điểm giảm nhanh hơn nhiều so với mức tăng khoảng cách: xa gấp khoảng 3 lần thì số điểm chỉ còn dưới 1/10. So với đường cong ở slide (xe con, trung vị: khoảng 1968 điểm ở 0–10 m, 718 ở 10–20 m, 214 ở 20–30 m, 72 ở 30–40 m, 19 ở 60–80 m), số của tôi cao hơn; giả thuyết: có thể hộp của tôi bao cả một ít điểm mặt đường hoặc vật sát bên xe, và mỗi khoảng chỉ có 1 xe nên chưa đại diện như trung vị của slide.

**Tự kiểm:**
- Nếu không sửa: `selfcheck` không cờ cuboid nào (0/90). Tôi xem lại ảnh trong `work/xem/` và thấy gán gần như đã chuẩn hết không thấy điểm sai sót gì, nên giữ nguyên các hộp. Tôi không sửa cuboid nào chỉ để tắt cờ.

**Đổi kiểm:**
- Nếu không có ai: không có bạn để đổi kiểm. Tôi tự đối chiếu 2 con số trong mục này với bảng A: `dist_m` = 3,14 m của s01f40 idx 1 và `dist_m` = 48,00 m của s02f31 idx 5: khớp.

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
**(a) Nhãn dùng để làm gì**

Để học được hình khối và khoảng cách thật trong không gian, model cần nhãn 3D tính bằng mét chứ không phải pixel vì kích thước pixel co giãn theo khoảng cách camera và góc nhìn, trong khi mét giữ đúng tỷ lệ vật lý để model ước lượng độ sâu và va chạm. Với những vật chỉ có vài điểm rời rạc, model cần quy tắc riêng như nới biên hộp bao hoặc giữ lại thay vì lọc bỏ vì thiếu điểm, để không bỏ sót vật thể nhỏ hay ở xa.

**(b) Cách dùng AI**
- **Công cụ:** Claude (Claude Code, trợ lý trong terminal).
- **Câu hỏi chính:** lệnh PowerShell để cài `.venv`, chạy `dry`, `task`, `sync`, `pack`, `check_submission.py`; cảnh báo lệch phiên bản CVAT 2.74.1 với cvat-sdk 2.83; hệ trục VF (vạch đỏ ngắn của cuboid là đầu xe, vạch xanh lá dài là +y, phía sau xe thu dữ liệu); tóm tắt guideline và danh sách 11 ảnh. AI có sửa tiêu đề README, tiêu đề báo cáo, `configs/lab.ini`.
- **Dùng kết quả thế nào:** chạy lệnh theo hướng dẫn rồi tự đọc kết quả. Mọi cuboid, quan sát, nhận xét và con số trong báo cáo do tôi tự vẽ, tự đọc trên CVAT, bảng A và phiếu tự kiểm.

**(c) Điều còn chưa chắc**

- Điều còn chưa chắc là trường hợp gần như quá mờ thì liệu có nên đánh box cho vật thể hay không hoặc trường hợp các tia khá rời rạc mà camera ở xa vẫn có thể thấy mờ mờ thì có đánh box hay không.
