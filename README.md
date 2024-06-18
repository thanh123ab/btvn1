# Thông Tin Sinh Viên

Mã SV : K215480106124

Họ Và Tên : Cao Đức Thành

Lớp: K57KMT

Tên đề tài: Quản lý cửa hàng tạp hóa gia đình


# Project csdl cho bài toán:

mô tả về bài toán: Để quản lý cửa hàng tạp hóa cần thiết kế cơ sở dữ liệu bao gồm các thông tin về nhân viên, khách hàng, sản phẩm, các hóa đơn, Doanh thu,....

# Chức Năng:

Bài toán quản lý tạp hóa gia đình nhằm đảm bảo quản lý hiệu quả và tối ưu hóa nguồn tài nguyên:

Quản lý thông tin nhà cung cấp : thêm , xóa , sửa thông tin, xem thông tin nhà cung cấp

quản lý thông tin xuất nhập hàng: Thêm, s hàng nhập vào, kiểm tra hàng (HSD), hóa đơn bán hàng và quản lý nguồn hàng còn trong cửa hàng 


# các bảng của hệ thống 

Bảng Nhân Viên (MANV,HOTEN,SODT,NGAYSINH,NGVL);

Bảng Khách Hàng(MANV, HOTEN, DCHI, SODT, NGSINH, NGDK, DOANHSO);

Bảng Sản Phẩm(MASP,TENSP,DVT,NUOCSX,GIA);

Bảng hóa đơn( SOHD, NGHD, MANV, TRIGIA);

Bảng chi tiết hóa đơn (SOHD, MASP, SL);

Bảng Nhà Cung Cấp (MANCC, TENNCC, DCHI, SDT);

