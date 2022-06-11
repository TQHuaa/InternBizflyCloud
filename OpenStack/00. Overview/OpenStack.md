# Giới thiệu về OpenStack
OpenStack là một phần mềm mã nguồn mở cho phép triển khai và quản lý cơ sở hạ tầng đám mây dưới dạng nền tảng dịch vụ (IaaS)[5]. OpenStack hỗ trợ cả triển khai đám mây riêng và công khai. Nó đáp ứng hai yêu cầu chính của đám mây: khả năng mở rộng lớn và đơn giản trong việc triển khai.

OpenStack có khả năng cấu hình cao: người dùng có thể chọn có hoặc không triển khai một số dịch vụ do phần mềm cung cấp. Cấu hình của mỗi thành phần cũng tùy thuộc vào người dùng và được thực hiện dễ dàng thông qua giao diện lập trình ứng dụng (API) mà công cụ cung cấp. Do đó, có nhiều cách khác nhau để sử dụng OpenStack, điều này làm cho nó trở thành một công cụ linh hoạt có thể hoạt động cùng với các phần mềm khác.

Một lý do khác để áp dụng OpenStack là nó hỗ trợ các hypervisor khác nhau (ví dụ: Xen, VMware hoặc máy ảo dựa trên hạt nhân [KVM]) và một số công nghệ ảo hóa (chẳng hạn như kim loại trần hoặc máy tính hiệu suất cao).

# Các module chính
## Keystone
Keystone là một dự án Openstack cung cấp các dịch vụ xác thực, mã thông báo, danh mục và chính sách để các dự án trong Openstack sử dụng cụ thể[6]. Nó triển khai API nhận dạng của Openstack và là một phần không thể thiếu. Keystone có các chức năng chính như quản lý user và những quyền mà user được phép làm, cung cấp các dịch vụ nhận dạng và xác thực, tạo các chính sách giữa user và dịch vụ. 

## Glance
Glance (Image Service) là dịch vụ hình ảnh cung cấp khả năng khám phá, đăng ký (đăng ký), truy xuất (thu thập) hình ảnh cho máy ảo[7]. OpenStack Glance là kho lưu trữ trung tâm cho image ảo. Glance cung cấp RESTful API cho phép truy vấn siêu dữ liệu hình ảnh VM cũng như thu thập các hình ảnh thực tế. Image VM có sẵn thông qua Glance có thể được lưu trữ trong nhiều vị trí khác nhau, từ hệ thống tệp đến hệ thống lưu trữ đối tượng như OpenStack Swift.

Trong Glance, hình ảnh được lưu trữ dưới dạng mẫu, được sử dụng để khởi chạy các phiên bản mới. Glance được thiết kế để trở thành một dịch vụ độc lập đối với người dùng cần tổ chức các hình ảnh đĩa ảo lớn. Glance cung cấp giải pháp end-to-end cho quản lý hình ảnh đĩa đám mây. Nó cũng có thể lấy các bản chụp nhanh từ phiên bản đang chạy để sao lưu máy ảo và các trạng thái của máy ảo.

## Nova - Compute
Nova là thành phần cốt lõi ban đầu của OpenStack. Từ cấp độ kiến trúc, nó được coi là một trong những thành phần phức tạp nhất của OpenStack[8]. Nova cung cấp dịch vụ tính toán trong OpenStack và quản lý các máy ảo theo yêu cầu dịch vụ của người dùng OpenStack. 

Điều làm cho Nova trở nên phức tạp là sự tương tác của nó với một số lượng lớn các dịch vụ OpenStack khác và các thành phần bên trong mà nó phải cộng tác để đáp ứng các yêu cầu của người dùng về việc chạy một máy ảo.

## Neutron-networking service 
Nova-conductor cung cấp quyền truy cập cơ sở dữ liệu để tính toán các nút. Ý tưởng đằng sau dịch vụ này là ngăn truy cập cơ sở dữ liệu trực tiếp từ các nút máy tính, do đó tăng cường bảo mật cơ sở dữ liệu trong trường hợp một trong các nút máy tính bị xâm phạm. Bằng cách thu nhỏ các thành phần chung của OpenStack, chúng tôi thấy rằng Nova tương tác với một số dịch vụ như Keystone để xác thực, Glance cho hình ảnh và Horizon cho giao diện web. Ví dụ, tương tác Glance là trung tâm; quy trình API có thể tải bất kỳ truy vấn nào lên Glance, trong khi nova-compute sẽ tải hình ảnh xuống để khởi chạy các phiên bản.

## Dashboard - Horizon 
Horizon là trang tổng quan web kéo tất cả các phần khác nhau lại với nhau từ hệ sinh thái OpenStack. Horizon cung cấp giao diện người dùng web cho các dịch vụ OpenStack. Hiện tại, nó bao gồm tất cả các dịch vụ OpenStack cũng như một số dự án được ươm tạo. Nó được thiết kế như một ứng dụng web không trạng thái và ít dữ liệu. Nó không làm gì khác hơn là bắt đầu các hành động trong các dịch vụ OpenStack thông qua các lệnh gọi API và hiển thị thông tin mà OpenStack trả về cho Horizon. Nó không giữ bất kỳ dữ liệu nào ngoại trừ thông tin phiên trong kho dữ liệu của chính nó. Nó được thiết kế để trở thành một triển khai tham chiếu có thể được tùy chỉnh và mở rộng bởi các nhà khai thác cho một đám mây cụ thể. Nó tạo thành nền tảng của một số đám mây công cộng, đáng chú ý nhất là HP Public Cloud và trung tâm của nó là cách tiếp cận mô-đun có thể mở rộng để xây dựng. Horizon dựa trên một loạt các mô-đun được gọi là bảng xác định sự tương tác của từng dịch vụ. Các mô-đun của nó có thể được bật hoặc tắt, tùy thuộc vào khả năng cung cấp dịch vụ của đám mây cụ thể. Ngoài tính linh hoạt về chức năng này, Horizon rất dễ tạo kiểu với Cascading Style Sheets (CSS).
