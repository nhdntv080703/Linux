# Linux

## Cài đặt yum local (cách sử dụng)

- Yum là 1 công cụ để quản lý các gói phần mềm trong hệ điều hành Linux. Nó rất linh hoạt và tiện lợi nếu như Server của bạn có kết nối ra Internet. Nhưng thường thì điều kiện không được lý tưởng như vậy: Các server trên thực tế thường không được kết nối ra ngoài Internet vì lý do bảo mật. Vậy để sử dụng yum để cài đăt các gói phần mềm thông thường mà không có kết nối Internet mình sẽ tạo repo yum.

Các bước tiến hành:
1. Bước 1: Mount DVD cài đặt Linux 
Đầu tiên, các bạn cần phải bỏ DVD cài đặt vào ổ CD/DVD của máy chủ. Sau đó hãy thực hiện lệnh sau để mount DVD vào thư mục /mnt/cdrom
# mkdir /mnt/cdrom
# mount /dev/cdrom /mnt/cdrom

Thư mục Package là thư mục lưu trữ các gói phần mềm có trong đĩa cài đặt Linux.
# cd /mnt/cdrom

Copy toàn bộ thư mục này sang 1 phân vùng khác.
# cp -R /mnt/cdrom/Packages /u02/

2. Bước 2: Cài đặt gói createrepo
Vào thư mục Packages và cài đặt gói createrepo (phiên bản tùy thuộc vào đĩa DVD bạn đang có)
# cd /u02/Packages
# rpm -Uvh createrepo-0.9.9-28.el7.noarch.rpm

3. Bước 3: Tạo Repository cho Yum
Sử dụng câu lệnh createrepo để tạo ra Reposity cho yum từ thư mục /mnt/cdrom/Packages

# createrepo -v /u02/Packages

Spawning worker 0 with 5210 pkgs
Worker 0: reading 389-ds-base-1.3.10.2-6.el7.x86_64.rpm
Worker 0: reading 389-ds-base-libs-1.3.10.2-6.el7.x86_64.rpm
.........

Tiếp theo, di chuyển vào thư mục /etc/yum.repos.d/

# cd /etc/yum.repos.d/

Và tạo 1 file có tên localrepo.repo có nội dung như sau

vi /etc/yum.repos.d/localrepo.repo

[localrepo]

name=Linux DVD

baseurl=file:///u02/Packages

gpgcheck=0

enabled=1

Trong đó, baseurl là đường dẫn đến thư mục chứa các gói Packages

4. Bước 4: Xác nhận lại Local Repository

Xóa cache của yum

# yum clean all

Loaded plugins: langpacks, ulninfo
Cleaning repos: cassandra localrepo ol7_UEKR6 ol7_developer_EPEL ol7_latest pgdg-common pgdg10 pgdg11 pgdg12 pgdg13 pgdg96 pgpool42

Gõ lệnh yum repolist để liệt kê các Repository đã được cấu hình
[root@lab02 Packages]# yum repolist

Loaded plugins: langpacks, ulninfo
cassandra/signature                                                                                                                                                          |  833 B  00:00:00
......
repolist: 72,907

Vậy là đã cấu hình thành công

 
[wp-svg-icons icon=”point-right” wrap=”i”] 

5. Bước 5: Kiểm thử
Để thử nghiệm, tắt mạng Internet đi, sau đó gõ lệnh yum
# yum install telnet
Loaded plugins: langpacks, ulninfo
Resolving Dependencies
--> Running transaction check
---> Package telnet.x86_64 1:0.17-65.el7_8 will be installed
--> Finished Dependency Resolution

....

Installed:
  telnet.x86_64 1:0.17-65.el7_8

Complete!

## Sử dụng RPM

1. RPM là gì
RPM(Red Hat Package Manager) là một công cụ dùng để quản lý gói mặc định và mã nguồn mở mặc định cho các hệ thống dựa trên Red Hat (RHEL, CentOS và Fedora). Công cụ này giúp cho phép chúng ta có thể cài đặt, cập nhật, gỡ cài đặt, truy vấn, xác minh và quản lý các gói phần mềm trên hệ thống.
Các file RPM được thiết kế để tải xuống và cài đặt độc lập, bên ngoài kho phần mềm
Chức năng cơ bản lệnh RPM:
• Install: Sử dụng để cài đặt bất kỳ gói RPM.
• Remove: Sử dụng để xóa hoặc hủy cài đặt bất kỳ gói RPM.
• Upgrade: Sử dụng để cập nhật gói RPM hiện có.
• Verify: Sử dụng để truy vấn bất kỳ gói RPM.
• Query: Sử dụng để xác minh các gói RPM.

2. Các lệnh sử dụng RPM trên linux

1. Cài đặt gói RPM
Để cài đặt một gói rpm bạn thêm tuỳ chọn -i để cài đặt. Bên dưới mình cài đặt một gói có tên là telnet-0.17-65.el7_8.x86_64.rpm
  
AZDIGI Tutorial
rpm -ivh telnet-0.17-65.el7_8.x86_64.rpm
    
Trong đó:
• -i : Cài đặt một gói
• -v : verbose hiển thị đẹp mắt hơn
• -h: hiển thị dấu # khi giải nén gói

2. Cách cài đặt gói RPM không phụ thuộc
Để cài đặt các gói RPM và bỏ quả các phần phụ thuộc bạn sử dụng lệnh và thêm tuỳ chọn như sau –nodeps
Ví dụ:
  
AZDIGI Tutorial
rpm -ivh --nodeps telnet-0.17-65.el7_8.x86_64.rpm
    

Lệnh trên bắt buộc cài đặt gói rpm bằng cách bỏ qua các lỗi phụ thuộc, nhưng nếu các tệp phụ thuộc đó bị thiếu, thì chương trình sẽ không hoạt động cho đến khi bạn cài đặt lại chúng.
3. Kiểm tra gói RPM đã cài đặt
Để kiểm tra gói đã cài đặt bạn sử dụng lệnh -q với tên gói.
Ví dụ mình tìm gói có tên là telnet
  
AZDIGI Tutorial
rpm -q telnet

Output
telnet-0.17-65.el7_8.x86_64
[root@monitor rpm]#
    
4. Liệt kê tất cả các file của gói RPM đã cài đặt
Để xem tất cả các file được cài đặt trong gói rpm bạn sử dụng lệnh rpm và tuỳ chọn -ql (query list).
  
AZDIGI Tutorial
rpm -ql telnet
    
5. Liệt kê tất cả các gói RPM được cài đặt
Để liệt kê tất cả các gói rpm đã được cài đặt và hệ thống linux bạn sử dụng lệnh rpm kèm tuỳ chọn -qa (query all)
  
AZDIGI Tutorial
rpm -qa
    
6. Nâng cấp gói RPM
Nếu bạn muốn nâng cấp một gói rpm đã cài đặt, bạn hãy sử dụng lệnh rpm kèm tuỳ chọn -U (Upgrade) và một trong những ưu điểm chính của việc sử dụng tùy chọn này là nó sẽ không chỉ nâng cấp phiên bản mới nhất của bất kỳ gói, mà còn duy trì bản sao lưu của gói cũ hơn để phòng trường hợp nếu gói nâng cấp mới hơn không chạy có thể được sử dụng lại được.
Ví dụ:
  
AZDIGI Tutorial
rpm -Uvh telnet-0.17-65.el7_8.x86_64.rpm
7. Cách xoá gói RPM
Để huỷ cài đặt hoặc xoá gói rpm bạn sử dụng lệnh rpm và tuỳ chọn -e để gở bỏ.
Ví dụ: Mình gở bỏ gói telnet
  
AZDIGI Tutorial
rpm -evv telnet
8. Truy vấn thông tin gói RPM đã cài đặt.
Để kiểm tra thông tin chi tiết gói rpm đã cài đặt bạn sử dụng tuỳ chọn -qi (query infomation) để xem chi tiết các thông tin về gói.
Ví dụ: Mình kiểm tra thông tin gói telnet đã cài đặt.
  
AZDIGI Tutorial
rpm -qi telnet

## Sử dụng wget

1. Tải một file đơn giản
Lệnh này sẽ download một file từ Internet về máy và lưu trữ nó trong thư mục hiện tại (nếu muốn biết bạn đang ở thư mục nào sử dụng lệnh pwd).
Khi được tải về trên terminal sẽ hiển thị các thông tin như quá trình tải về, kích thước file, ngày giờ tải về trong khi tải cho chúng ta.
1
# wget http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz
2. Tải file với một tên khác
Sử dụng -O (viết hoa) để tải file với tên file mà bạn muốn lưu.
1
# wget -O wget.zip http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz
Như ở trên thì ta sẽ có được một file tải về có tên là wget.zip
3. Tải nhiều file với giao thức HTTP và FTP
Chúng ta sẽ xem cách tải nhiều file sử dụng giao thức HTTP và FTP với một lệnh wget được thực hiện như thế nào nhé.
1
# wget http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz ftp://ftp.gnu.org/gnu/wget/wget-1.10.1.tar.gz.sig
4. Đọc địa chỉ URL từ một file có sẵn
Bạn có thể lưu trữ một địa chỉ URL trong một file và sau đó download nó sử dụng lựa chọn là -i.
Bên dưới mình đã tạo một file tmp.txt trong thư mục wget, nơi mà ta sẽ lưu trữ địa chỉ URL để tải về.
1
# wget -i /wget/tmp.txt
5.Tiếp tục tải về khi chưa hoàn tất
Khi bạn đang tải một file có kích thước lớn nhưng không may có sự cố xảy ra thì nó sẽ dừng việc tải xuống. Trong trường này nếu bạn muốn tiếp tục tải phần còn lại của file đó thì chúng ta sử dụng tùy chọn -c.
Nhưng nếu bạn tải một file mà không có -c thì wget sẽ thêm .1 vào phần mở rộng ở cuối file, và xem đó như một bản tải xuống mới. Vì vậy, cách tốt nhất là thêm -c vào khi bạn muốn tải một file có kích thước lớn.
1
# wget -c http://centos-hcm.viettelidc.com.vn/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
6. Tải file với việc nối .1 vào tên file
Khi bạn bắt đầu tải xuống mà không có lựa chọn -c thì lệnh wget sẽ thêm .1 vào cuối file và bắt đầu với việc tải một file mới. Nếu file .1 đã tồn tại thì file .2 sẽ được nối vào cuối của file.
1
# wget http://centos-hcm.viettelidc.com.vn/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
Chúng ta thấy .1 đã được nối vào cuối của file.
1
2
3
4
# ls -l CentOS*
 
-rw-r--r--. 1 root root 3877262 Oct 2 12:47 CentOS-7-x86_64-DVD-2009.iso
-rw-r--r--. 1 root root 181004 Oct 2 12:50 CentOS-7-x86_64-DVD-2009.iso.1
7. Tải file trong background
Chúng tôi sẽ nói sơ qua background là gì để bạn hiểu, khi bạn thực hiện một hành động hay còn gọi một tiến trình trong linux thì bạn có 2 cách để chạy nó, đó là background process và foreground process.
Lợi thế của việc chạy một tiến trình trong background là bạn có thể chạy có lệnh khác mà không phải đợi tới khi nó kết thúc mới bắt đầu một tiến trình mới.
Trong lệnh wget chúng ta muốn tải một file trong background thì sử dụng lựa chọn -b, sau khi tải xong nó sẽ ngay lập tức được ghi vào trong file /wget/log.txt.
1
2
3
# wget -b /wget/log.txt http://centos-hcm.viettelidc.com.vn/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
 
Continuing in background, pid 3550.
8. Hạn chế giới hạn tốc độ tải xuống
Với lựa chọn là -limit-race=100k, giới hạn tốc độ tải xuống là 100k và nó sẽ được lưu vào file /wget/log.txt như hình bên dưới.
1
# wget -c --limit-rate=100k /wget/log.txt http://centos-hcm.viettelidc.com.vn/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
9. Hạn chế download FTP và HTTP với username và password
Với lựa chọn -http-user=username, -http-password=password, và -ftp-user=username, -ftp-password=password, bạn có thể tải xuống các website bị hạn chế mật khẩu như hình bên dưới.
1
# wget --http-user=tenten --http-password=password http://centos-hcm.viettelidc.com.vn/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
10. Kiểm tra phiên bản hiện tại của Wget và lệnh Help
Với lựa chọn là -version, bạn có thể xem phiên bản hiện tại của wget và -help nếu bạn cần được giúp đỡ thêm về lệnh wget.
1
2
3
4
# wget --version
 
 
# wget --help


## Sử dụng LVM

1. Thao tác tạo#
Lưu ý : Nếu phân vùng được mount vào thư mục root rồi thì không thể tạo physical colume
Tạo physical volume
• Ta sử dụng lệnh pvcreate theo cú pháp
• pvcreate /dev/(tên phân vùng)

Ta kiểm tra lại bằng lệnh pvs xem ta tạo được thành công physical volume hay chưa

Tạo một Group volume
• Ta sử dụng lệnh vgcreate theo cú pháp
• vgcreate (ten_group) /dev/(tên phân vùng 1) /dev/(tên phân vùng 2)
Ta sử dụng lệnh vgs để kiểm tra xem group volume.

Tạo một Logical volume theo cú pháp
lvcreate -L size_volume -n (ten logical) (tên group volume)
Để kiểm tra logical volume thì ta sử dụng lệnh lvs

Sau khi tạo xong một logical thì sẽ phải định dạng xong một logical để có thể mount nó vào cây thư mục root như trong phần lệnh mount tôi đã hướng dẫn thực hiện mount một phân vùng thì ta mới có thể sử dụng được logical này.
2. Thay đổi dung lượng#
Thay đổi dung lượng physical volume ta sử dụng lệnh theo cú pháp
lvextend -L (n) /dev/(tên group)/(tên logical)
Trong đó
• lvextend : là lệnh tăng dung lượng
• lvreduce : là lệnh dùng để giảm dung lượng
• -L : là option của lệnh
• (n) : là số dùng để tăng giảm dung lượng theo ý muốn của ta
Sau khi ta thay đổi dung lượng như ta muốn thì ta sử dụng lệnh resize2fs để xác nhận thay đổi
resize2fs (tên group volume)(tên logical volume)
ở đây tôi sẽ làm một kịch bảnvề việc thay đổi dung lượng. Đầu tiên tôi sẽ chọn ra logical mà tôi muốn thay đổi sau đó tôi sẽ thay đổi nó rồi kiểm tra lại xem nó thay đổi hay là chưa. sau khi thay đổi về dung lượng thì ta cần phải mount vào để có thể sử dụng nó.

Muốn tăng dung lượng thì ta làm giống như với giảm dung lượng chỉ cần thay đổi lệnh lvreduce thành lệnh lvextend
Thay đổi dung lượng của một group volume
Khi thay đổi dung lượng của một group volume thì ta sẽ thêm hoặc xóa phân vùng thuộc group để có thể thay đổi dung lượng của nó.
Đầu tiên ta kiểm tra xem có phân vùng nào chưa thuộc group thì ta sẽ thêm phân vùng đó vào một group là cách để tăng kích thước cho group đó
Tôi sẽ thêm vdb3 vào group g_volume
Đầu tiên ta kiểm tra dung lượng của group

vgextend /dev/g_volume /dev/vdc2

ta kiểm tra lại dung lượng của group bằng lệnh vgs một lần nữa và thấy sự thay đổi của nó

3.Thao tác xóa#
Xóa một logical ta sử dụng lệnh theo cú pháp
lvremove /dev/(ten group)/(ten logical)
Đầu tiên ta kiểm tra xem có những logical nào

Ở đây tôi chọn xóa logical cuối cùng khoanh đỏ

ở dòng cuối cùng đã ghi xóa thành công logical
Xóa một group volume ta thực hiện theo cú pháp
vgremove /dev/(tên group)
Đầu tiên tôi kiểm tra xem có những group volume nào sau đó chọn ra một group. Ở đây tôi chọn xóa g_volume rồi kiểm tra lại xem nó đã bị xóa hay chưa.

Xóa một physical volume ta thưc hiện theo cú pháp
pvremove /dev/(tên physical)



