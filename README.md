![image](https://github.com/thanh123ab/btvn1/assets/168660300/1cc88aec-71ef-4c7e-bde1-84440c8977af)# Thông Tin Sinh Viên

Mã SV : K215480106124

Họ Và Tên : Cao Đức Thành

Lớp: K57KMT

Tên đề tài: Quản lý cửa hàng tạp hóa gia đình


# Project csdl cho bài toán:

mô tả về bài toán: Để quản lý cửa hàng tạp hóa cần thiết kế cơ sở dữ liệu bao gồm các thông tin về nhân viên, khách hàng, sản phẩm, các hóa đơn, Doanh thu,....

# Chức Năng:

Bài toán quản lý tạp hóa gia đình nhằm đảm bảo quản lý hiệu quả và tối ưu hóa nguồn tài nguyên:

Quản lý thông tin nhà cung cấp : thêm , xóa , sửa thông tin, xem thông tin nhà cung cấp

quản lý thông tin xuất nhập hàng: Thêm,  hàng nhập vào, kiểm tra hàng (HSD), hóa đơn bán hàng và quản lý nguồn hàng còn trong cửa hàng 



# tạo cơ sở dữ liệu gồm các bảng

tạo database:
```
CREATE DATABASE QuanLy;
GO
-- Sử dụng cơ sở dữ liệu QuanLy
USE QuanLy;
GO
```
Bảng khách hàng :
```
CREATE TABLE KHACHHANG
(
    MAKH CHAR(4) PRIMARY KEY,
    HOTEN VARCHAR(40),
    DCHI VARCHAR(50),
    SODT VARCHAR(20),
    NGSINH SMALLDATETIME,
    NGDK SMALLDATETIME,
    DOANHSO MONEY
);
```
>- **MAKH**: Trường MAKH được định nghĩa là khóa chính (Primary Key) với tính tự tăng (`(1,1)`), tức là giá trị sẽ tự động tăng mỗi khi có bản ghi mới được thêm vào bảng.
>- **HOTEN**: là họ tên của khách hàng. Đây là trường để xác định duy nhất tên với mỗi khách hàng.
>- **DCHI** : địa chỉ của khách hàng.
>- **NGSINH**:ngày sinh của khách hàng với kiểu dữ liệu ngày và giờ có phạm vi từ 01/01/1900 đến 06/06/2079, với độ chính xác đến phút.
>- **NGDK** : Ngày đăng ký của khách hàng.
>- **DOANHSO**: là tổng doanh số hoặc số tiền mà khách hàng đã chi tiêu.

Bảng hóa đơn( SOHD, NGHD, MANV, TRIGIA);
```
CREATE TABLE HOADON
(
    SOHD INT PRIMARY KEY,
    NGHD SMALLDATETIME,
    MAKH CHAR(4),
    MANV CHAR(4),
    TRIGIA MONEY,
    FOREIGN KEY (MAKH) REFERENCES KHACHHANG(MAKH),
    FOREIGN KEY (MANV) REFERENCES NHANVIEN(MANV)
);

```
>- **SOHD**: PRIMARY KEY xác định rằng cột SOHD là khóa chính của bảng, đảm bảo mỗi giá trị trong cột này là duy nhất và không null.
>- **NGHD**: là ngày hóa đơn, chỉ định ngày mà hóa đơn được tạo.
>- **MAKH**: là mã khách hàng, liên kết hóa đơn với khách hàng cụ thể.
>- **MANV**: là mã nhân viên, liên kết hóa đơn với nhân viên cụ thể.
>- **TRIGIA**:  là tổng trị giá của hóa đơn, biểu thị tổng số tiền của các mặt hàng trong hóa đơn.
>- **FOREIGN KEY**: Định nghĩa ràng buộc khóa ngoại để đảm bảo tính toàn vẹn tham chiếu dữ liệu giữa các bảng. Trường `MAKH` tham chiếu đến `MAKH` trong bảng ` KHACHHANG`, và trường `MANV` tham chiếu đến `MANV` trong bảng `MANV`. 

Bảng chi tiết hóa đơn (SOHD, MASP, SL);
```
CREATE TABLE CTHD
(
    SOHD INT,
    MASP CHAR(4),
    SL INT,
    PRIMARY KEY (SOHD, MASP),
    FOREIGN KEY (SOHD) REFERENCES HOADON(SOHD),
    FOREIGN KEY (MASP) REFERENCES SANPHAM(MASP)
);

```

Bảng Nhà Cung Cấp (MANCC, TENNCC, DCHI, SDT);
```
CREATE TABLE NCC
(
    MANCC CHAR(4) PRIMARY KEY,
    TENNCC VARCHAR(40),
    DCHI VARCHAR(50),
    SODT VARCHAR(20)
);

```

Bảng Sản Phẩm ( MASP, TENSP, DVT, NUOCSX, HSD, GIA);
```
CREATE TABLE SANPHAM
(
    MASP CHAR(4) PRIMARY KEY,
    TENSP VARCHAR(40),
    DVT VARCHAR(20),
    NUOCSX VARCHAR(40),
    HSD DATETIME,
    GIA MONEY
);

```
Bảng tồn kho ( MaSP, SoLuong)
```
CREATE TABLE TonKho
(
    MaSP CHAR(4) PRIMARY KEY,
    SoLuong INT
);
```
ta có các bảng liên kết lại với nhau như sau : 
![image](https://github.com/thanh123ab/btvn1/assets/168660300/7c1b6209-0df3-4b68-8c28-a78dc4b25305)

Thêm dữ liệu cho các bảng :
```
-- Nhập thông tin khách hàng
INSERT INTO KHACHHANG (MAKH, HOTEN, DCHI, SODT, NGSINH, NGDK, DOANHSO)
VALUES
('KH01', 'Nguyen Van A', '123 Le Loi', '0123456789', '1980-01-01', '2023-01-01', 1000000),
('KH02', 'Tran Thi B', '456 Nguyen Hue', '0987654321', '1990-02-01', '2023-02-01', 2000000),
('KH03', 'Le Van C', '789 Tran Hung Dao', '0234567890', '1975-03-01', '2023-03-01', 1500000);

-- Nhập thông tin nhân viên
INSERT INTO NHANVIEN (MANV, HOTEN, SODT, NGAYSINH)
VALUES
('NV01', 'Nguyen Van X', '0987654321', '1990-01-01'),
('NV02', 'Tran Thi Y', '0987654321', '1995-02-01'),
('NV03', 'Le Van Z', '0987654321', '1992-03-01');

-- Nhập giá trị cho sản phẩm
INSERT INTO SANPHAM (MASP, TENSP, DVT, NUOCSX, GIA)
VALUES
('SP01', 'Sua Tuoi', 'Hop', 'Vietnam', 15000),
('SP02', 'Banh Mi', 'Chiec', 'Vietnam', 5000),
('SP03', 'Nuoc Ngot', 'Chai', 'Vietnam', 10000),
('SP04', 'Bot Giat', 'Tui', 'Vietnam', 5000),
('SP05', 'Dau An', 'Chai', 'Vietnam', 5000);

-- Nhập giá trị hóa đơn
INSERT INTO HOADON (SOHD, NGHD, MAKH, MANV, TRIGIA)
VALUES
(1, '2024-06-18', 'KH01', 'NV01', 30000),
(2, '2024-06-19', 'KH02', 'NV02', 20000),
(3, '2024-06-20', 'KH03', 'NV03', 15000);

-- Nhập giá trị cho chi tiết hóa đơn (CTHD)
INSERT INTO CTHD (SOHD, MASP, SL)
VALUES
(1, 'SP01', 2),
(1, 'SP02', 1),
(2, 'SP02', 2),
(2, 'SP03', 1),
(3, 'SP01', 1),
(3, 'SP03', 1);
-- Nhập dữ liệu cho bảng TonKho
INSERT INTO TonKho (MaSP, SoLuong)
VALUES
('SP01', 100),
('SP02', 200),
('SP03', 150),
('SP04', 80),
('SP05', 120),
('SP06', 50);
-- Nhập giá trị cho Nhà cung cấp
INSERT INTO NCC (MANCC, TENNCC, DCHI, SODT)
VALUES
('NC01', 'Nha Cung Cap A', '123 Phan Chu Trinh', '0321456789'),
('NC02', 'Nha Cung Cap B', '456 Le Thanh Ton', '0345678910'),
('NC03', 'Nha Cung Cap C', '789 Tran Phu', '0367891234');
```
 ## Tạo các chức năng
 **1.  Tạo các thủ tục đối với nhà cung cấp**
 Xử lý chức năng thêm , xóa , sửa thông tin, xem thông tin nhà cung cấp
 ```
CREATE PROCEDURE themNCC
    @MANCC NVARCHAR(50),
    @TENNCC NVARCHAR(50),
    @DCHI NVARCHAR(50),
    @SODT INT
AS
BEGIN
    INSERT INTO NCC (MANCC, TENNCC, DCHI, SODT)
    VALUES (@MANCC, @TENNCC, @DCHI, @SODT);
END;
GO
-- Xóa nhà cung cấp
CREATE PROCEDURE XoaNCC
    @MANCC NVARCHAR(50)
AS
BEGIN
    DELETE FROM NCC
    WHERE MANCC = @MANCC;
END;
GO

-- Sửa thông tin nhà cung cấp
CREATE PROCEDURE CapNhatNCC
    @MANCC NVARCHAR(50),
    @TENNCC NVARCHAR(50),
    @DCHI NVARCHAR(50),
    @SODT INT
AS
BEGIN
    UPDATE NCC
    SET TENNCC = @TENNCC, DCHI = @DCHI, TENNCC = @TENNCC
    WHERE MANCC = @MANCC;
END;
GO
-- Xem thông tin nhà cung cấp
SELECT * FROM NCC;
```
kiểm tra với các thủ tục
```
-- thêm ncc
EXEC themNCC @MANCC = 'NC04', @TENNCC = N'Nhà Cung Cap D', @DCHI = N'123 Nguyen Trai', @SODT = '0398765432';
-- xóa ncc
EXEC XoaNCC @MANCC = 'NC04';
--sửa thông tin ncc
EXEC CapNhatNCC @MANCC = 'NC03', @TENNCC = N'Nhà Cung Cap C - Updated', @DCHI = N'789 Tran Phu - Updated', @SODT = '0367891234';
-- xem thông tin nhà cc
EXEC XemNCC;
```
hình ảnh sau khi thêm ncc :![image](https://github.com/thanh123ab/btvn1/assets/168660300/6334cbd3-1fc4-46a1-aecb-e6448f33895a)


sửa :![image](https://github.com/thanh123ab/btvn1/assets/168660300/826a99b2-1700-456d-b63f-5e0f30750461)


xóa:![image](https://github.com/thanh123ab/btvn1/assets/168660300/89924f5e-c615-4dca-a1e3-65fdc875316b)


quản lý thông tin xuất nhập hàng: Thêm,  hàng nhập vào, kiểm tra hàng (HSD), hóa đơn bán hàng
```
-- Thêm sản phẩm nhập vào
CREATE PROCEDURE themSANPHAM
    @MASP CHAR(4),
    @TENSP VARCHAR(40),
    @DVT VARCHAR(20),
    @NUOCSX VARCHAR(40),
    @HSD DATETIME,
    @GIA MONEY
AS
BEGIN
    INSERT INTO SANPHAM(MASP,TENSP, DVT, NUOCSX, HSD, GIA)
    VALUES (@MASP, @TENSP, @DVT, @NUOCSX,@HSD, @GIA);
END;
GO

-- Kiểm tra hàng hóa hết hạn sử dụng (HSD)
SELECT * FROM SANPHAM WHERE HSD < GETDATE();

-- Tạo hóa đơn bán hàng mới
CREATE PROCEDURE ThemHoaDonBanmoi
    @SOHD INT,
    @NGHD SMALLDATETIME,
    @MAKH CHAR(4),
    @MANV CHAR(4),
    @TRIGIA MONEY
AS
BEGIN
   INSERT INTO HOADON(SOHD, NGHD, MAKH,MANV, TRIGIA) 
    VALUES (@SOHD, @NGHD, @MAKH, @MANV, @TRIGIA)
END;
GO
```
kiểm tra thủ tục:
```
-- Thêm hóa đơn mới
EXEC ThemHoaDonBanmoi @SOHD = 4, @NGHD = '2024-06-21', @MAKH = 'KH01', @MANV = 'NV01', @TRIGIA = 35000;
```

Trigger cập nhật hàng tồn kho sau khi thêm chi tiết hóa đơn
```
CREATE TRIGGER tr_UpdateTonKho
ON CTHD
AFTER INSERT
AS
BEGIN
UPDATE TonKho
SET SoLuong = SoLuong - (SELECT SL FROM inserted WHERE TonKho.MaSP = inserted.MASP)
FROM TonKho
INNER JOIN inserted ON TonKho.MaSP = inserted.MASP;
END;
GO -- Kết thúc batch chứa trigger
-- Trigger cập nhật doanh thu khi tạo hóa đơn mới
CREATE TRIGGER tr_CapNhatDoanhThu
ON HOADON
AFTER INSERT
AS
BEGIN
-- Lấy ngày của hóa đơn mới
DECLARE @NgayHoaDon DATE = (SELECT CAST(NGHD AS DATE) FROM inserted);
-- Kiểm tra ngày có trong doanh thu
IF NOT EXISTS (SELECT 1 FROM DoanhThu WHERE NgayDoanhThu = @NgayHoaDon)
BEGIN
    -- Nếu chưa có, thêm mới vào bảng DoanhThu
    INSERT INTO DoanhThu (NgayDoanhThu, TongDoanhThu)
    VALUES (@NgayHoaDon, 0);
END

-- Cập nhật doanh thu cho ngày đó
UPDATE DoanhThu
SET TongDoanhThu = TongDoanhThu + (SELECT TRIGIA FROM inserted)
WHERE NgayDoanhThu = @NgayHoaDon;END;
GO 
-- Xem hàng tồn kho sau khi bán hàng
SELECT * FROM TonKho;
```
kiểm tra trigger hoạt động: 
```
CREATE TRIGGER tr_CapNhatDoanhThu
ON HOADON
AFTER INSERT
AS
BEGIN
-- Lấy ngày của hóa đơn mới
DECLARE @NgayHoaDon DATE = (SELECT CAST(NGHD AS DATE) FROM inserted);
-- Kiểm tra xem ngày đó đã có trong bảng DoanhThu chưa
IF NOT EXISTS (SELECT 1 FROM DoanhThu WHERE NgayDoanhThu = @NgayHoaDon)
BEGIN
    -- Nếu chưa có, thêm mới vào bảng DoanhThu
    INSERT INTO DoanhThu (NgayDoanhThu, TongDoanhThu)
    VALUES (@NgayHoaDon, 0)
END

-- Cập nhật doanh thu cho ngày đó
UPDATE DoanhThu
SET TongDoanhThu = TongDoanhThu + (SELECT TRIGIA FROM inserted)
WHERE NgayDoanhThu = @NgayHoaDon;END;
GO 
-- Xem hàng tồn kho sau khi bán hàng
SELECT * FROM TonKho;
```
kiểm tra trigger theo ngày
```
-- Xem doanh thu theo ngày
SELECT NgayDoanhThu, TongDoanhThu FROM DoanhThu;
```
![image](https://github.com/thanh123ab/btvn1/assets/168660300/b83fca09-6ece-4589-9489-4f58685d8fdf)

Xem tổng doanh thu trong khoảng thời gian nhất định
```
SELECT SUM(TongDoanhThu) AS TongDoanhThu
FROM DoanhThu
WHERE NgayDoanhThu BETWEEN '2024-06-01' AND '2024-06-30';
```
![image](https://github.com/thanh123ab/btvn1/assets/168660300/a52b8c7b-1bef-483f-b21b-c8cb1675a349)
