# **HƯỚNG DẪN TRIỂN KHAI WINDOWS SERVER**

# **PHẦN 1: CÀI ĐẶT VÀ CẤU HÌNH CƠ BẢN**

## **1. Cài đặt Windows Server**

- **Bước 1: Chọn phiên bản Windows Server.**
    
    Chọn Windows Server 2025 Standard làm phiên bản để cài đặt. Đây là phiên bản phổ biến cho môi trường doanh nghiệp nhỏ đến trung bình, hỗ trợ các tính năng cơ bản như Active Directory, DNS, DHCP và Storage Spaces, với cải tiến về bảo mật và hiệu suất so với phiên bản trước (như hỗ trợ 32k-page database cho AD DS).
    
    **Link:** https://www.microsoft.com/en-us/windows-server/pricing
    
    ![***Giải thích chi phí cấp phép:** Phiên bản Windows Server 2025 sử dụng mô hình cấp phép dựa trên lõi CPU (core-based licensing), yêu cầu ít nhất 16 lõi cho mỗi máy chủ vật lý. Chi phí MSRP cho giấy phép 16 lõi khoảng **$1,176 USD**, cộng thêm CAL (Client Access License) cho mỗi người dùng hoặc thiết bị truy cập (ví dụ: gói CAL khoảng **$200-400 USD** tùy loại). Chi phí này giúp đảm bảo tuân thủ bản quyền, hỗ trợ cập nhật từ Microsoft, và có thể thay đổi tùy nhà cung cấp. Kiểm tra chi tiết tại trang Microsoft hoặc reseller.*](/image/image.png)
    
    ***Giải thích chi phí cấp phép:** Phiên bản Windows Server 2025 sử dụng mô hình cấp phép dựa trên lõi CPU (core-based licensing), yêu cầu ít nhất 16 lõi cho mỗi máy chủ vật lý. Chi phí MSRP cho giấy phép 16 lõi khoảng **$1,176 USD**, cộng thêm CAL (Client Access License) cho mỗi người dùng hoặc thiết bị truy cập (ví dụ: gói CAL khoảng **$200-400 USD** tùy loại). Chi phí này giúp đảm bảo tuân thủ bản quyền, hỗ trợ cập nhật từ Microsoft, và có thể thay đổi tùy nhà cung cấp. Kiểm tra chi tiết tại trang Microsoft hoặc reseller.*
    

---

- **Bước 2: Thực hiện cài đặt máy ảo với Desktop Experience (DE).**
    
    ![***Mục đích:** DE cung cấp giao diện đồ họa (GUI) đầy đủ, dễ quản lý cho người mới, hỗ trợ các ứng dụng cần GUI.*](/image/0153b0d7-b563-4341-9885-f872afebbd39.png)
    
    ***Mục đích:** DE cung cấp giao diện đồ họa (GUI) đầy đủ, dễ quản lý cho người mới, hỗ trợ các ứng dụng cần GUI.*
    
    ![*Cài đặt hoàn tất Windows Server Desktop Experience (DE) 2025*](/image/image%201.png)
    
    *Cài đặt hoàn tất Windows Server Desktop Experience (DE) 2025*
    

---

- **Bước 3: Thực hiện cài đặt máy ảo với phiên bản Core.**
    
    ![*Mục đích: Core là phiên bản nhẹ, không GUI, phù hợp cho môi trường sản xuất để tiết kiệm tài nguyên và tăng bảo mật.*](/image/image%202.png)
    
    *Mục đích: Core là phiên bản nhẹ, không GUI, phù hợp cho môi trường sản xuất để tiết kiệm tài nguyên và tăng bảo mật.*
    
    ![*Cài đặt hoàn tất Windows Server Core 2025*](/image/image%203.png)
    
    *Cài đặt hoàn tất Windows Server Core 2025*
    

---

- **Bước 4: Phân tích và so sánh DE và Core.**
    
    
    | Tiêu chí | Windows Server DE | Windows Server Core |
    | --- | --- | --- |
    | **Tính năng** | Có GUI đầy đủ (Server Manager, MMC), hỗ trợ media và công cụ đồ họa. | Không GUI, chỉ dòng lệnh/PowerShell; thiếu tính năng không cần thiết. |
    | **Yêu cầu tài nguyên** | Cao hơn (hơn RAM, CPU, disk space do GUI). | Thấp hơn (tiết kiệm ~2-4 GB disk, ít CPU/RAM), tăng hiệu suất. |
    | **Bảo mật** | Bề mặt tấn công lớn hơn do mã code nhiều. | Bề mặt tấn công nhỏ hơn, ít lỗ hổng hơn nhờ loại bỏ GUI. |
    | **Quản lý** | Dễ dàng trực tiếp trên máy. | Chủ yếu từ xa, khó hơn cho người mới. |
    | **Ứng dụng hỗ trợ** | Hỗ trợ hầu hết ứng dụng cần GUI. | Không hỗ trợ một số ứng dụng GUI-based. |
    
    **Mục đích:** So sánh giúp hiểu ưu nhược điểm để chọn phiên bản phù hợp (DE cho phát triển, Core cho sản xuất).
    

---

- **Bước 5:  Cách quản trị Core bằng công cụ GUI từ xa.**
    - **Windows Admin Center (WAC):** Cài đặt WAC trên máy client (tải từ Microsoft), kết nối đến Core qua IP. Hỗ trợ quản lý qua browser (dashboard, PowerShell từ xa).
    - **Remote Server Administration Tools (RSAT):** Cài trên Windows client (qua Settings > Apps > Optional features > Add RSAT tools). Sử dụng Server Manager hoặc MMC để kết nối và quản lý Core.
    - **Microsoft Management Console (MMC):** Từ client, mở MMC, thêm snap-in (như Computer Management), kết nối đến Core qua IP.
    
    **Mục đích:** Các công cụ này cho phép quản lý GUI mà không cần GUI trên Core, tăng tính linh hoạt và bảo mật.
    
    ---
    
- **Bước 6: Cấu hình và chứng minh quản trị từ xa (sử dụng Server Manager/MMC)**
    1. **Trên máy Core:**
        - Đăng nhập và gõ lệnh `sconfig`.
        - Chọn tùy chọn `4) Configure Remote Management` và chọn `1) Enable Remote Management`.
    2. **Trên máy Vinh_Phu_PDC:**
        - Mở **Server Manager**.
        - Nhấp chuột phải vào "All Servers" -> "Add Servers".
        - Trong tab "Active Directory", tìm và thêm máy chủ Core.
        
        ![image.png](/image/image%204.png)
        
        ![image.png](/image/image%205.png)
        

---

## **2. Cấu hình cơ bản và bảo mật**

- **Bước 1: Cấu hình múi giờ, tên máy, IP tĩnh.**
    
    ![***Mục đích:** Đảm bảo thời gian đồng bộ (cho AD), tên máy theo quy tắc (dễ quản lý), IP tĩnh (ổn định kết nối).*](/image/image%206.png)
    
    ***Mục đích:** Đảm bảo thời gian đồng bộ (cho AD), tên máy theo quy tắc (dễ quản lý), IP tĩnh (ổn định kết nối).*
    
    ![image.png](/image/image%207.png)
    

---

- **Bước 2: Triển khai 5 biện pháp bảo mật cơ bản cho máy chủ Windows Server.**
    1. **Cấu hình Windows Firewall:** 
        - **Mục tiêu:** Tạo quy tắc (rule) trong Firewall để chặn các gói tin ICMP Echo Request (lệnh ping) từ bên ngoài đi vào máy chủ, giúp tăng cường bảo mật cơ bản.
        - **Các bước thực hiện:**
            - **Mở:** `wf.msc`.
            - **Tạo Rule:** Inbound Rule -> New Rule.
            - **Loại Rule:** Custom.
            - **Giao thức:** ICMPv4.
            - **Tùy chỉnh (Customize):** Chỉ chọn loại `Echo Request`.
            - **Hành động (Action):** Block the connection.
            - **Kết quả:** Tạo rules để chặn ping hoàn toàn.
            
            ![image.png](/image/image%208.png)
            
    2. **Vô hiệu hóa dịch vụ không cần thiết:** 
        - Nhấn `Windows + R`, gõ `services.msc` và nhấn Enter.
            
            Xác định Dịch vụ không cần thiết dựa trên Vai trò (Role) của Máy chủ
            
            Việc một dịch vụ có "*cần thiết*" hay không phụ thuộc hoàn toàn vào vai trò mà máy chủ đó đang đảm nhiệm.
            
            Các dịch vụ sau đây thường an toàn để vô hiệu hóa trên hầu hết các máy chủ nếu không có nhu cầu sử dụng cụ thể:
            
            - **Print Spooler:** Nếu máy chủ không phải là máy chủ in (Print Server) hoặc không bao giờ kết nối với máy in. *Lưu ý: Vô hiệu hóa dịch vụ này sẽ làm cho việc in ấn không thể thực hiện được.*
                
                ![image.png](/image/image%209.png)
                
            - **Telephony:** Cần cho các kết nối dial-up hoặc qua mạng điện thoại. Hầu hết các máy chủ hiện đại không cần dịch vụ này.
                
                ![image.png](/image/image%2010.png)
                
            - **Remote Registry:** Cho phép người dùng từ xa chỉnh sửa registry. Vô hiệu hóa dịch vụ này giúp tăng cường bảo mật.
                
                ![image.png](/image/image%2011.png)
                
            - **Downloaded Maps Manager:** Dịch vụ dùng cho ứng dụng bản đồ, thường không cần thiết trên máy chủ.
                
                ![image.png](/image/image%2012.png)
                
            
    3. **Cập nhật hệ điều hành:** Chạy Windows Update
        
        ![***Mục đích:** Vá lỗ hổng bảo mật.*](/image/image%2013.png)
        
        ***Mục đích:** Vá lỗ hổng bảo mật.*
        
    4. **Thiết lập chính sách mật khẩu mạnh:**
        - **Mục đích:** Ngăn chặn tấn công dò mật khẩu (brute-force).
        - **Triển khai:** Mở `Local Security Policy` (`secpol.msc`) > `Account Policies > Password Policy`. Cấu hình các yêu cầu như `Minimum password length`, `Password must meet complexity requirements`. (Lưu ý: Sau khi lên domain, chính sách này sẽ bị GPO của domain ghi đè).
            
            ![image.png](/image/image%2014.png)
            
    5. **Cấu hình User Account Control (UAC):**
        
        User Account Control (UAC) là một lớp bảo vệ cốt lõi của Windows, được thiết kế để ngăn chặn phần mềm độc hại tự ý thực hiện các thay đổi quan trọng trên hệ thống. Dưới đây là giải thích chi tiết từng chức năng, đánh giá mức độ quan trọng và cấu hình đề xuất để đạt được sự cân bằng giữa bảo mật và tiện dụng.
        
        - **Triển khai:** Trong `Local Security Policy`, đi tới `Local Policies > Security Options`. Tìm các chính sách bắt đầu bằng "User Account Control" và đảm bảo chúng được bật và cấu hình ở mức an toàn (ví dụ: "Prompt for consent for non-Windows binaries").
        
        ![image.png](/image/image%2015.png)
        
        ---
        
        ### ## Các Chính Sách Quan Trọng Nhất và Cấu Hình Đề Xuất
        
        Đây là những chính sách có ảnh hưởng lớn nhất đến cách UAC hoạt động. Bạn nên ưu tiên cấu hình đúng các mục này.
        
        ### 1. `User Account Control: Run all administrators in Admin Approval Mode`
        
        - **Chức năng:** Đây là **công tắc tổng** của UAC. Khi được bật, ngay cả khi bạn đăng nhập bằng tài khoản Administrator, các ứng dụng vẫn chạy với quyền hạn của người dùng thông thường. Khi một tác vụ đòi hỏi quyền quản trị, UAC sẽ được kích hoạt để yêu cầu sự cho phép.
        - **Mức độ quan trọng:** **Cực kỳ quan trọng.**
        - **Cấu hình đề xuất:** **Enabled (Bật)**. Tắt chính sách này sẽ vô hiệu hóa gần như toàn bộ chức năng bảo vệ của UAC cho tài khoản quản trị, tạo ra một lỗ hổng bảo mật lớn.
        
        ### 2. `User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode`
        
        - **Chức năng:** Quyết định loại thông báo mà **tài khoản quản trị (Administrator)** sẽ thấy khi một ứng dụng yêu cầu quyền cao hơn.
            - `Elevate without prompting`: Không hỏi, tự động cấp quyền. **(Rất nguy hiểm)**
            - `Prompt for credentials`: Yêu cầu nhập lại mật khẩu. **(An toàn nhất nhưng hơi phiền phức)**
            - `Prompt for consent`: Hiển thị hộp thoại Yes/No. **(Mặc định, cân bằng tốt)**
            - `Prompt for consent for non-Windows binaries`: Chỉ hỏi Yes/No cho các ứng dụng không phải của Microsoft. **(Lựa chọn tốt và tiện lợi)**
        - **Mức độ quan trọng:** **Rất quan trọng.**
        - **Cấu hình đề xuất:** **Prompt for consent for non-Windows binaries**. Đây là thiết lập cân bằng nhất giữa an toàn và tiện lợi. Bạn vẫn được cảnh báo khi phần mềm bên thứ ba muốn thay đổi hệ thống, nhưng không bị làm phiền bởi các tác vụ của chính Windows.
        
        ### 3. `User Account Control: Behavior of the elevation prompt for standard users`
        
        - **Chức năng:** Quyết định thông báo mà **người dùng thông thường (Standard User)** sẽ thấy.
            - `Automatically deny elevation requests`: Tự động từ chối mọi yêu cầu nâng quyền.
            - `Prompt for credentials`: Yêu cầu người dùng nhập tên và mật khẩu của một tài khoản quản trị để tiếp tục.
        - **Mức độ quan trọng:** **Rất quan trọng.**
        - **Cấu hình đề xuất:** **Prompt for credentials (Mặc định)**. Cấu hình này đảm bảo rằng người dùng thông thường không thể tự ý cài đặt phần mềm hay thay đổi hệ thống nếu không có sự cho phép (bằng mật khẩu) của quản trị viên.
        
        ### 4. `User Account Control: Switch to the secure desktop when prompting for elevation`
        
        - **Chức năng:** Khi được bật, màn hình sẽ mờ đi và chỉ hiển thị duy nhất hộp thoại UAC. Đây được gọi là "màn hình an toàn" (Secure Desktop), nó ngăn chặn các phần mềm độc hại khác tương tác hoặc giả mạo cú nhấp chuột vào nút "Yes" của bạn.
        - **Mức độ quan trọng:** **Rất quan trọng.**
        - **Cấu hình đề xuất:** **Enabled (Bật)**. Tắt tính năng này sẽ làm giảm đáng kể mức độ bảo mật của UAC.
        
        ---
        
        ### ## Giải Thích Chi Tiết Các Chính Sách Khác
        
        Đây là các chính sách tinh chỉnh bổ sung, thường bạn có thể giữ nguyên giá trị mặc định.
        
        - **`User Account Control: Detect application installations and prompt for elevation`**
            - **Chức năng:** Tự động phát hiện các tệp cài đặt (ví dụ: `setup.exe`, `.msi`) và kích hoạt UAC để hỏi quyền trước khi chạy.
            - **Cấu hình đề xuất:** **Enabled (Bật)**. Đây là chức năng cốt lõi giúp kiểm soát việc cài đặt phần mềm.
        - **`User Account Control: Admin Approval Mode for the Built-in Administrator account`**
            - **Chức năng:** Áp dụng chế độ UAC cho tài khoản "Administrator" tích hợp sẵn (tài khoản này thường bị vô hiệu hóa theo mặc định).
            - **Cấu hình đề xuất:** **Enabled (Bật)**. Để phòng trường hợp bạn cần sử dụng tài khoản này, nó vẫn sẽ được UAC bảo vệ.
        - **`User Account Control: Only elevate executables that are signed and validated`**
            - **Chức năng:** Tăng cường bảo mật bằng cách chỉ cho phép các tệp thực thi có chữ ký số hợp lệ được nâng quyền.
            - **Cấu hình đề xuất:** **Disabled (Tắt)** cho hầu hết người dùng. Bật tính năng này có thể ngăn chặn một số phần mềm hợp pháp nhưng không có chữ ký số (ví dụ: các công cụ quản trị nhỏ, phần mềm cũ) hoạt động. Chỉ nên bật trong môi trường yêu cầu an ninh rất cao.
        - **`User Account Control: Allow UIAccess applications to prompt for elevation without using the secure desktop`**
            - **Chức năng:** Cho phép các ứng dụng hỗ trợ người dùng khuyết tật (UI Access, ví dụ: trình đọc màn hình) yêu cầu quyền mà không cần chuyển sang màn hình an toàn.
            - **Cấu hình đề xuất:** **Disabled (Tắt)** trừ khi bạn có nhu cầu sử dụng các công cụ hỗ trợ đặc biệt.
        - **`User Account Control: Virtualize file and registry write failures to per-user locations`**
            - **Chức năng:** Đây là một tính năng tương thích. Khi một ứng dụng cũ (không nhận biết UAC) cố gắng ghi dữ liệu vào một thư mục hệ thống được bảo vệ (như `C:\Program Files`), Windows sẽ chuyển hướng hành động ghi đó đến một thư mục ảo trong hồ sơ của người dùng.
            - **Cấu hình đề xuất:** **Enabled (Bật)**. Điều này giúp các phần mềm cũ hoạt động tốt hơn mà không cần cấp quyền quản trị cho chúng.
        
        Tóm lại, **các thiết lập mặc định của Windows đã khá an toàn và cân bằng**. Bạn chỉ nên thay đổi chúng khi thực sự hiểu rõ tác động của từng chính sách.
        

---

# **PHẦN 2: TRIỂN KHAI CÁC DỊCH VỤ CHÍNH**

## 1. Dịch vụ Active Directory Domain Services (AD DS) & DNS

### **1.1. Triển khai 2 x DC**

- **Cài đặt vai trò AD DS trên máy Windows Server DE:**
    1. Trong **Server Manager**, chọn `Manage > Add Roles and Features`.
    2. Đi qua các bước của wizard cho đến phần `Server Roles`.
    3. Check vào ô **Active Directory Domain Services**. Một cửa sổ pop-up sẽ hiện ra yêu cầu thêm các feature liên quan (như DNS), nhấn `Add Features`.
    4. Hoàn tất wizard và nhấn `Install`.
        
        ![image.png](/image/image%2016.png)
        
- **Nâng cấp máy chủ thành Domain Controller (Promote):**
    1. Sau khi cài đặt xong, trong Server Manager, sẽ thấy một thông báo cờ vàng. Nhấp vào đó và chọn `Promote this server to a domain controller`.
    2. Wizard "Active Directory Domain Services Configuration Wizard" sẽ mở ra. Đây là bước quan trọng cần giải thích các tùy chọn.
        
        **Các tùy chọn Deployment Operation và giải thích**
        
        - **Add a domain controller to an existing domain:** Dùng để thêm một Domain Controller bổ sung (ADC) vào một domain đã tồn tại. Đây là lựa chọn để tăng tính sẵn sàng và cân bằng tải. (Ta sẽ dùng tùy chọn này cho máy Core sau).
        - **Add a new domain to an existing forest:** Dùng để tạo một domain con (child domain) hoặc một domain tree mới trong một forest đã có. Ví dụ: tạo domain `hcm.jetking.local` khi đã có `jetking.local`.
        - **Add a new forest:** Dùng để tạo ra Domain Controller đầu tiên, thiết lập một forest và một domain gốc (root domain) hoàn toàn mới.
        
        **Lựa chọn cho PDC:** Chọn **Add a new forest**. Đặt tên domain, ví dụ: `jetking.local`.
        
    3. Ở màn hình tiếp theo, đặt mật khẩu `Directory Services Restore Mode (DSRM)`. Đây là mật khẩu dùng để khôi phục AD trong trường hợp khẩn cấp.
    4. Các bước tiếp theo wizard sẽ tự động cấu hình DNS. Cứ để mặc định.
    5. Kiểm tra lại và nhấn `Install`. Máy chủ sẽ tự khởi động lại.
        
        ![image.png](/image/image%2017.png)
        
        ![image.png](/image/image%2018.png)
        
- **Cài đặt vai trò AD DS và Promote ADC trên Windows Server Core:**
    1. Trên **Windows Server Core** trong giao diện `sconfig` chọn option 1 để tham gia domain
    2. Thực hiện các bước Cài đặt vai trò AD DS và Promote ADC trên **Vinh_Phu_ADC** **(máy Core)** như trên **Vinh_Phu_PDC (máy DE)**
        
        ![image.png](/image/image%2019.png)
        
        ![image.png](/image/image%2020.png)
        
        ![image.png](/image/image%2021.png)
        

---

### **1.2. Group Policy Object (GPO)**

1. Trên Vinh_Phu_PDC, mở **Group Policy Management** (`gpmc.msc`).
2. Tạo một OU mới tên là `PhongIT` và tạo một user `user01` trong OU đó.
3. Tạo một GPO mới và liên kết (link) nó vào OU `PhongIT`. Đặt tên là `PhongIT_Policies`.
    
    ![image.png](/image/image%2022.png)
    
- **1.2.1. Vô hiệu hóa USB storage drive:**
    - Edit GPO `PhongIT_Policies`.
    - Đi đến: `Computer Configuration > Policies > Administrative Templates > System > Removable Storage Access`.
    - Tìm policy `All Removable Storage classes: Deny all access`, chọn `Enabled`.
        
        ![image.png](/image/image%2023.png)
        
        ![image.png](/image/image%2024.png)
        
- **1.2.2. Thiết lập chính sách mật khẩu và lockout:**
    - Edit GPO `Default Domain Policy`. Đây là nơi tốt nhất để cấu hình chính sách toàn domain.
    - Đi đến `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies`.
    - Trong `Password Policy`, cấu hình:
        - **Minimum password length** (Độ dài tối thiểu của mật khẩu)
            - Đặt số ký tự tối thiểu cho mật khẩu.
            - Giá trị khuyến nghị là **ít nhất 8 ký tự**.
        - **Password must meet complexity requirements** (Mật khẩu phải đáp ứng yêu cầu phức tạp)
            - Chính sách này yêu cầu mật khẩu phải bao gồm ít nhất 3 trong 4 loại ký tự: chữ hoa, chữ thường, số, và ký tự đặc biệt.
            - Nên **Enable (Bật)** chính sách này.
        - **Enforce password history** (Lịch sử mật khẩu)
            - Chính sách này ngăn người dùng sử dụng lại các mật khẩu cũ.
            - Nên đặt giá trị là **24**, có nghĩa là hệ thống sẽ lưu lại 24 mật khẩu cuối cùng của người dùng và họ không thể sử dụng lại trong số đó.
                
                ![image.png](/image/b70cb5b5-0f81-4c74-96af-53ca042ac684.png)
                
                ![image.png](/image/image%2025.png)
                
    - Trong `Account Lockout Policy`, cấu hình:
        - **Account lockout threshold** (Ngưỡng khóa tài khoản):
            - Đặt số lần nhập sai mật khẩu tối đa trước khi tài khoản bị khóa.
            - Giá trị khuyến nghị là từ **3 đến 5 lần**. Việc đặt giá trị quá cao sẽ dễ bị tấn công brute-force, còn quá thấp sẽ gây phiền toái cho người dùng.
            - Khi cấu hình chính sách này, hai chính sách còn lại sẽ tự động được gợi ý cấu hình.
        - **Account lockout duration** (Thời gian khóa tài khoản):
            - Đặt thời gian (tính bằng phút) tài khoản sẽ bị khóa sau khi đạt đến ngưỡng khóa.
            - Có thể đặt là **30 phút** hoặc **0** nếu muốn tài khoản bị khóa vĩnh viễn cho đến khi có quản trị viên mở khóa.
        - **Reset account lockout counter after** (Thời gian đặt lại bộ đếm khóa tài khoản):
            - Đặt thời gian (tính bằng phút) để hệ thống xóa bộ đếm số lần nhập sai mật khẩu.
            - Giá trị này nên nhỏ hơn hoặc bằng **Account lockout duration**. Ví dụ, nếu đặt là **30 phút**, sau 30 phút nhập sai, bộ đếm sẽ trở về 0.
                
                ![image.png](/image/image%2026.png)
                
                ![image.png](/image/image%2027.png)
                
- **1.2.3. Cài đặt phần mềm:**
    - Tạo một thư mục chia sẻ trên Vinh_Phu_PDC (ví dụ: `\\Vinh_Phu_PDC\Software`) và cấp quyền `Read` cho `Authenticated Users` và `Read` cho Everyone trong tab `Security`
    - Đặt file cài đặt `.msi` (ví dụ: 7-Zip.msi) vào thư mục này.
    - Edit GPO `PhongIT_Policies`.
    - Đi đến `User Configuration > Policies > Software Settings > Software installation`.
    - Chuột phải -> `New > Package...`. Trỏ đến đường dẫn UNC của file .msi (`\\Vinh_Phu_PDC\Software\7z.msi`).
    - **Giải thích tùy chọn:**
        - **Published:** Người dùng có thể tùy chọn cài đặt phần mềm từ `Add/Remove Programs` trong Control Panel.
        - **Assigned:** Phần mềm sẽ tự động được cài đặt khi người dùng đăng nhập hoặc sẽ xuất hiện trên Start Menu như thể đã được cài, và sẽ được cài khi người dùng nhấp vào lần đầu.
        - **Advanced:** Cho phép tùy chỉnh sâu hơn.
    - Chọn `Assigned`.
    - Start -> Run -> nhập lệnh gpupdate /force ⇒ Cập nhật chính sách
        
        ![image.png](/image/image%2028.png)
        
        ![Screenshot 2025-08-13 165213.png](/image/Screenshot_2025-08-13_165213.png)
        
- **1.2.4. Chặn công cụ quản trị:**
    - Edit GPO `PhongBanA_Policies`.
    - Đi đến `User Configuration > Policies > Administrative Templates > System`.
    - Tìm policy `Don't run specified Windows applications`, chọn `Enabled`. Nhấn `Show...` và thêm vào danh sách: `cmd.exe`, `powershell.exe`.
    - Đi đến `User Configuration > Policies > Administrative Templates > Control Panel`.
    - Tìm policy `Prohibit access to Control Panel and PC settings`, chọn `Enabled`.
        
        ![image.png](/image/image%2029.png)
        
        ![image.png](/image/image%2030.png)
        
    
    ![Screenshot 2025-08-13 171206.jpg](/image/Screenshot_2025-08-13_171206.jpg)
    
    ![image.png](/image/image%2031.png)
    
    ![image.png](/image/image%2032.png)
    

---

### **1.3. FSMO Roles**

- **Liệt kê 5 vai trò FSMO và chức năng:**
    1. **Schema Master:** Quản lý và chịu trách nhiệm cập nhật lược đồ (schema) của Active Directory. Lược đồ định nghĩa tất cả các đối tượng và thuộc tính trong AD.
    2. **Domain Naming Master:** Chịu trách nhiệm thêm và xóa domain khỏi forest. Đảm bảo tên domain là duy nhất.
    3. **PDC Emulator (Primary Domain Controller Emulator):** Đóng vai trò là máy chủ thời gian chính trong domain, xử lý các thay đổi mật khẩu ngay lập tức, và hoạt động như một DC "chính" cho các ứng dụng cũ.
    4. **RID Master (Relative ID Master):** Phân phát các khối RID cho các DC khác trong domain. Mỗi đối tượng trong AD (user, group, computer) có một SID (Security ID) duy nhất, và RID là một phần của SID đó.
    5. **Infrastructure Master:** Chịu trách nhiệm cập nhật thông tin về các đối tượng từ các domain khác (cross-domain object references).
    
    - **Liệt kê 5 vai trò FSMO và chức năng:**
        
        Mở PowerShell trên **Vinh_Phu_PDC** và gõ các lệnh sau:
        
        ```powershell
        # Xem các vai trò cấp domain
        Get-ADDomain | Select-Object PDCEmulator, RIDMaster, InfrastructureMaster
        
        # Xem các vai trò cấp forest
        Get-ADForest | Select-Object SchemaMaster, DomainNamingMaster
        ```
        
        ![image.png](/image/image%2033.png)
        
    - **Phân bổ lại các vai trò (Transfer):**
        - **Mục đích:** Để tăng khả năng chịu lỗi, không nên để tất cả các vai trò trên một DC duy nhất. Ta sẽ di chuyển 2 vai trò cấp forest sang **Vinh_Phu_ADC**.
        - Mở PowerShell trên **Vinh_Phu_PDC** và chạy lệnh:
            
            ```powershell
            Move-ADDirectoryServerOperationMasterRole -Identity "Vinh_Phu_ADC" -OperationMasterRole SchemaMaster, DomainNamingMaster
            ```
            
        - Chạy lại các lệnh kiểm tra ở trên để chứng minh 2 vai trò đã được chuyển sang **Vinh_Phu_ADC**.
            
            ![image.png](/image/image%2034.png)
            
    - **Kế hoạch Seizing FSMO:**
        
        **KẾ HOẠCH ỨNG PHÓ KHI DC GIỮ FSMO ROLE BỊ HỎNG (SEIZING FSMO ROLES)**
        
        > Tình huống giả định: **Vinh_Phu_PDC** (đang giữ 3 FSMO roles: PDC, RID, Infrastructure) bị hỏng hoàn toàn và không thể phục hồi.
        > 
        
        > Mục tiêu: Cưỡng chiếm (seize) 3 vai trò này và chuyển về cho **Vinh_Phu_ADC**.
        > 
        
        **Cảnh báo:** Chỉ thực hiện Seize khi DC cũ **chắc chắn không bao giờ được kết nối lại** vào mạng(mô phỏng tắt card mạng). Nếu không sẽ gây xung đột nghiêm trọng.
        
        **Các bước thực hiện:**
        
        1. **Xác minh sự cố:** Đảm bảo `Vinh_Phu_PDC` không thể truy cập được (ping, RDP không thành công) và không có khả năng khởi động lại.
        2. **Đăng nhập vào DC còn lại:** Đăng nhập vào `Vinh_Phu_ADC` bằng tài khoản Domain Admin.
        3. **Thực hiện Seizing:** Mở PowerShell với quyền Administrator và chạy lệnh:
            
            ```powershell
            Move-ADDirectoryServerOperationMasterRole -Identity "Vinh_Phu_ADC" -OperationMasterRole PDCEmulator, RIDMaster, InfrastructureMaster -Force
            ```
            
            Tham số `-Force` chính là hành động "Seize".
            
        4. **Kiểm tra lại:** Chạy lại lệnh `Get-ADDomain` và `Get-ADForest` để xác nhận tất cả 5 vai trò hiện đã thuộc về `Vinh_Phu_ADC`.
            
            ![image.png](/image/image%2035.png)
            
        
        1. **Dọn dẹp Metadata** bằng `ntdsutil`
            
            Sau khi Seize thành công, phải xóa thông tin về DC đã hỏng khỏi Active Directory để ngăn ngừa sự cố.
            
            Quy trình dọn dẹp metadata của Domain Controller đã hỏng, sử dụng công cụ dòng lệnh **`ntdsutil`**.
            
            ### **Quy trình gỡ bỏ Domain Controller đã chết (Metadata Cleanup)**
            
            1. **Đăng nhập vào Vinh_Phu_ADC** với quyền Administrator. 
            2. **Mở Command Prompt hoặc PowerShell** với quyền Administrator. 
            3. **Khởi chạy `ntdsutil`:**
                - Nhập
                    
                    `ntdsutil` và nhấn `Enter`. 
                    
                - (Tùy chọn) Nhập
                    
                    `?` để xem các lệnh trợ giúp. 
                    
            4. **Truy cập chế độ `metadata cleanup`:**
                - Nhập
                    
                    `metadata cleanup` và nhấn `Enter`. 
                    
                - (Tùy chọn) Nhập
                    
                    `?` để xem các lệnh trợ giúp trong chế độ này. 
                    
            5. **Thiết lập kết nối với máy chủ đích (Vinh_Phu_ADC ):**
                - Nhập
                    
                    `connections` và nhấn `Enter`. 
                    
                - (Tùy chọn) Nhập
                    
                    `?` để xem các lệnh trợ giúp. 
                    
                - **Đặt thông tin xác thực:** Nhập `set creds jetking.local administrator *` và nhấn `Enter`.
                    - Khi được yêu cầu, nhập mật khẩu của tài khoản Administrator cho domain `jetking.local`.
                - **Kết nối đến miền:** Nhập `connect to domain jetking.local` và nhấn `Enter`.
                    - Bạn sẽ thấy thông báo:
                    - "Binding to \\Vinh_Phu_ADC.jetking.local as jetking.local\administrator…"
                    - "Connected to \\Vinh_Phu_ADC.jetking.local as jetking.local\administrator."
                - **Thoát khỏi chế độ `server connections`:** Nhập `quit` và nhấn `Enter`.
            6. **Chọn Site, Domain, và Server để dọn dẹp:**
                - Bạn đã quay lại chế độ `metadata cleanup:`. Nhập
                    
                    `select operation target` và nhấn `Enter`. 
                    
                - (Tùy chọn) Nhập
                    
                    `?` để xem các lệnh trợ giúp.
                    
                - **Liệt kê các Site:** Nhập `list sites` và nhấn `Enter`.
                    - Ghi lại số thứ tự của Site mà DC1 thuộc về.
                - **Chọn Site:** Nhập `select site <số thứ tự site>` (ví dụ: `select site 0` nếu Site của bạn là số 0) và nhấn `Enter`.
                - **Liệt kê các Domain trong Site:** Nhập `list domains in site` và nhấn `Enter`.
                    - Ghi lại số thứ tự của tên miền của bạn (ví dụ: `jetking.local`).
                - **Chọn Domain:** Nhập `select domain <số thứ tự domain>` (ví dụ: `select domain 0` nếu tên miền của bạn là số 0) và nhấn `Enter`.
                - **Liệt kê các Server trong Domain và Site đã chọn:** Nhập `list servers for domain in site` và nhấn `Enter`.
                    - Ghi lại số thứ tự của DC1 (máy chủ đã chết) trong danh sách này.
                - **Chọn Server đã chết:** Nhập `select server <số thứ tự server đã chết>` (ví dụ: `select server 0` nếu DC1 là số 0) và nhấn `Enter`.
                - **Thoát khỏi chế độ `select operation target`:** Nhập `quit` và nhấn `Enter`.
            7. **Thực hiện dọn dẹp siêu dữ liệu:**
                - Bạn đã quay lại chế độ
                    
                    `metadata cleanup:`. 
                    
                - (Tùy chọn) Nhập
                    
                    `?` để xem các lệnh trợ giúp.
                    
                - **Gỡ bỏ Server đã chọn:** Nhập `remove selected server` và nhấn `Enter`.
                    - Một hộp thoại xác nhận sẽ xuất hiện, hỏi bạn có chắc chắn muốn xóa không. Click `Yes`.
                    - Bạn sẽ thấy thông báo xác nhận rằng máy chủ đã được gỡ bỏ thành công.
            8. **Xác minh và Thoát khỏi `ntdsutil`:**
                - (Tùy chọn) Để kiểm tra lại, bạn có thể nhập
                    
                    `select operation target` -> `list servers for domain in site` để xác nhận rằng DC1 không còn trong danh sách. 
                    
                - **Thoát khỏi chế độ `metadata cleanup`:** Nhập `quit` và nhấn `Enter`.
                - **Thoát khỏi `ntdsutil`:** Nhập `quit` và nhấn `Enter` một lần nữa để thoát hoàn toàn.
            
            Sau khi hoàn tất, thông tin về DC1 đã chết sẽ được loại bỏ khỏi Active Directory, giúp môi trường mạng sạch sẽ và ổn định hơn.
            
            ![image.png](/image/image%2036.png)
            
            ![image.png](/image/image%2037.png)
            

---

### **1.4. Delegation Control**

1. Trong `Active Directory Users and Computers`, tạo một user mới tên `helpdesk_user` và một OU mới tên `NhanVien`.
2. Di chuyển `user01` vào OU `NhanVien`.
3. Chuột phải vào OU `NhanVien` -> `Delegate Control...`.
4. Wizard sẽ mở ra. Nhấn `Next`.
5. `Add...` -> thêm `helpdesk_user` vào.
6. Ở màn hình `Tasks to Delegate`, chọn các tác vụ phổ biến:
    - **Create, delete, and manage user accounts**
    - **Reset user passwords and force password change at next logon**
7. Hoàn tất wizard.
    
    ![image.png](/image/image%2038.png)
    
    "Tại bước này, mình đã ủy quyền hai tác vụ chính cho tài khoản `helpdesk_user` trên OU `NhanVien`:
    
    - **Create, delete, and manage user accounts:** Cấp quyền cho `helpdesk_user` có thể tạo, xóa, và quản lý các tài khoản người dùng. Tác vụ này bao gồm cả quyền **bật và tắt tài khoản người dùng**, giúp giảm tải các công việc quản lý cơ bản cho quản trị viên cấp cao."
    - **Reset user passwords and force password change at next logon:** Cho phép `helpdesk_user` đặt lại mật khẩu của người dùng, đồng thời buộc họ phải thay đổi mật khẩu đó trong lần đăng nhập kế tiếp.
        
        ![image.png](/image/image%2039.png)
        
        ![image.png](/image/image%2040.png)
        
    
    ---
    

### **1.5. DNS**

- **Cấu hình Zone:**
    1. Mở **DNS Manager** trên Vinh_Phu_PDC.
    2. Bạn sẽ thấy **Forward Lookup Zones** đã tự động được tạo cho `jetking.local`. Zone này ánh xạ tên máy thành địa chỉ IP.
    3. Tạo **Reverse Lookup Zone**:
        - Chuột phải vào `Reverse Lookup Zones` -> `New Zone...`.
        - Chọn `Primary zone` và check `Store the zone in Active Directory`.
        - **Giải thích tùy chọn Replicate:**
            - `To all DNS servers running on domain controllers in this forest`: Sao chép zone đến mọi DC trong cả forest.
            - `To all DNS servers running on domain controllers in this domain`: Sao chép đến mọi DC trong domain hiện tại. (Lựa chọn tốt nhất).
            - `To all domain controllers in this domain (for Windows 2000 compatibility)`: Tùy chọn cũ.
        - Chọn `To all DNS servers running on domain controllers in this domain`.
        - Chọn `IPv4 Reverse Lookup Zone`.
        - Nhập `Network ID`: `192.168.1`.
        - Hoàn tất wizard.
            
            ![image.png](/image/image%2041.png)
            
- **Tạo bản ghi (Records):**
    - Trong Forward Zone `jetking.local`, kiểm tra xem đã có bản ghi `A` cho `Vinh_Phu_PDC` và `Vinh_Phu_ADC` chưa.
    - Trong Reverse Zone `1.168.192.in-addr.arpa`, các bản ghi `PTR` tương ứng cũng sẽ tự động được tạo nếu bạn cho phép cập nhật động. Nếu chưa có, chuột phải và tạo mới. Bản ghi PTR ánh xạ IP về lại tên máy.
        
        ![image.png](/image/image%2042.png)
        
- **Kiểm tra phân giải (resolve):**
    - Join một máy client Windows 10/11 vào domain `jetking.local`.
    - Mở `cmd` trên máy client.
    - Gõ lệnh: `nslookup Vinh_Phu_PDC.jetking.local`. Kết quả phải trả về IP `192.168.1.10`.
    - Gõ lệnh: `nslookup 192.168.1.10`. Kết quả phải trả về tên `Vinh_Phu_PDC.jetking.local`.
        
        ![Screenshot 2025-08-14 220809.jpg](/image/Screenshot_2025-08-14_220809.jpg)
        

---

### 2. Dịch vụ Dynamic Host Configuration Protocol (DHCP)

**2.1. Cài đặt DHCP Server và Authorization**

1. **Cài đặt:** Trên cả 2 máy chủ DC (PDC và ADC), sử dụng `Add Roles and Features` (trên DE) hoặc `Install-WindowsFeature -Name DHCP -IncludeManagementTools` (trên Core) để cài đặt vai trò DHCP.
    
    ![image.png](/image/image%2043.png)
    
2. **Authorization:**
    - **Mục đích:** Trong môi trường Active Directory, một máy chủ DHCP phải được "ủy quyền" (authorize) để có thể bắt đầu cấp phát IP. Điều này ngăn chặn các máy chủ DHCP giả mạo (rogue DHCP) trong mạng.
    - Trên Vinh_Phu_PDC, mở **DHCP** console.
    - Bạn sẽ thấy tên máy chủ của mình có biểu tượng màu đỏ.
    - Chuột phải vào tên máy chủ -> `Authorize`. Sau vài giây, biểu tượng sẽ chuyển sang màu xanh.
    
    ![image.png](/image/image%2044.png)
    

**2.2. Cấu hình**

- **Tạo Scope trên Vinh_Phu_PDC:**
    1. Trong DHCP console, chuột phải vào `IPv4` -> `New Scope...`.
    2. Đặt tên cho scope (ví dụ: `VanPhong_Scope`).
    3. **IP Address Range:** Nhập dải IP sẽ cấp, ví dụ:
        - Start IP: `192.168.1.100`
        - End IP: `192.168.1.200`
        - Subnet mask: `255.255.255.0`
    4. **Add Exclusions:** Thêm dải IP không muốn cấp trong scope, ví dụ `192.168.1.150` đến `192.168.1.155`.
    5. **Lease Duration:** Để mặc định 8 ngày.
    6. **Configure DHCP Options:** Chọn `Yes, I want to configure these options now`.
        - **Router (Default Gateway):** Nhập `192.168.1.1`.
        - **Domain Name and DNS Servers:** Domain `jetking.local` sẽ tự điền. DNS Server sẽ tự nhận `192.168.1.10` và `192.168.1.11`.
    7. **Activate Scope:** Chọn `Yes, I want to activate this scope now`.
        
        ![image.png](/image/image%2045.png)
        
        ![image.png](/image/image%2046.png)
        
- **Thực hiện Reservation:**
    1. **Mục đích:** Đảm bảo một thiết bị cụ thể (ví dụ: máy in) luôn nhận được cùng một địa chỉ IP.
    2. Tìm địa chỉ MAC của máy client.
    3. Trong DHCP console, vào `Scope > Reservations`.
    4. Chuột phải -> `New Reservation...`.
    5. Nhập tên, địa chỉ IP muốn cấp (ví dụ: `192.168.1.99`) và địa chỉ MAC của client.
        
        ![image.png](/image/image%2047.png)
        
        ![image.png](/image/image%2048.png)
        
        | Tùy chọn | Chức năng và Giải thích ngắn gọn |
        | --- | --- |
        | Reservation name | Tên đặt chỗ: Một tên gợi nhớ để dễ dàng quản lý (ví dụ: HP_Printer_Phong_Ban_HR). |
        | IP address | Địa chỉ IP được đặt chỗ: Địa chỉ IP tĩnh mà bạn muốn gán vĩnh viễn cho thiết bị. Địa chỉ này phải nằm trong dải IP của scope nhưng không được nằm trong dải địa chỉ được cấp phát động để tránh xung đột. |
        | MAC address | Địa chỉ MAC: Địa chỉ vật lý của card mạng thiết bị. Bạn phải nhập chính xác chuỗi 12 ký tự này. Bạn có thể sử dụng dấu gạch ngang (-) hoặc không. |
        | Description | Mô tả: Thêm một mô tả chi tiết hơn về thiết bị để dễ dàng quản lý và xác định sau này. |
        | Supported types | Loại được hỗ trợ: Chọn loại thiết bị mà bạn muốn cấp IP. Tùy chọn mặc định là Both (cả DHCP và BOOTP) thường được sử dụng và phù hợp với hầu hết các thiết bị hiện đại. |

**2.3. Cấu hình DHCP Failover**

- **Mục đích của DHCP Failover:**
    - **Tính sẵn sàng cao (High Availability):** DHCP Failover đảm bảo rằng dịch vụ cấp phát địa chỉ IP sẽ không bị gián đoạn ngay cả khi một trong hai máy chủ DHCP gặp sự cố (như bị hỏng, tắt máy, mất điện, v.v.).
- **Thực hiện:**
    1. Trên **Vinh_Phu_PDC**, trong DHCP console, chuột phải vào `IPv4` -> `Configure Failover...`.
    2. Wizard sẽ hiện ra. Chọn scope bạn muốn cấu hình failover.
    3. **Partner Server:** Nhập tên của máy chủ DHCP thứ hai (`Vinh_Phu_ADC`).
    4. **Giải thích các tùy chọn Failover Mode:**
        - **Load balance:** Cả hai máy chủ đều chủ động cấp phát IP cho client. Tải được chia sẻ giữa chúng (mặc định 50-50). Đây là chế độ tốt nhất khi cả hai server đều hoạt động trong cùng một mạng.
        - **Hot standby:** Một máy chủ là server chính (Active), máy còn lại là server dự phòng (Standby). Server dự phòng chỉ hoạt động khi server chính bị lỗi. Chế độ này phù hợp khi server dự phòng đặt ở một site khác.
    5. **Lựa chọn:** Chọn **Load balance**.
    6. Tạo một `Shared Secret` (mật khẩu) để hai server giao tiếp an toàn.
    7. Hoàn tất wizard.
        
        ![image.png](/image/image%2049.png)
        
    
    ![image.png](/image/image%2050.png)
    
    ![image.png](/image/image%2051.png)
    
    ![image.png](/image/image%2052.png)
    
    ![image.png](/image/image%2053.png)
    

---

# PHẦN 3: CẤU HÌNH LƯU TRỮ

## Cấu hình Storage Spaces

- **Chuẩn bị:** Trên máy ảo **Vinh_Phu_PDC**, tắt máy và thêm 3 ổ đĩa ảo mới (Virtual Disk), mỗi ổ khoảng 60GB. Khởi động lại máy.
    
    ![image.png](/image/image%2054.png)
    
- **Thực hiện:**
    1. Trong **Server Manager**, đi đến `File and Storage Services > Storage Pools`.
    2. Sẽ thấy 3 ổ đĩa mới trong `Primordial Pool`.
        
        ![image.png](/image/image%2055.png)
        
    3. **Tạo Storage Pool:**
        - Trong ô `STORAGE POOLS`, nhấp vào `TASKS > New Storage Pool...`.
        - Đặt tên cho Pool (ví dụ: `MyDataPool`).
        - Chọn 3 ổ đĩa vật lý bạn vừa thêm vào Pool.
        - Hoàn tất việc tạo Pool.
            
            ![image.png](/image/image%2056.png)
            
    4. **Tạo Virtual Disk (Storage Space):**
        - Sau khi tạo Pool, wizard tạo Virtual Disk sẽ tự động chạy. Nếu không, chuột phải vào Pool vừa tạo và chọn `New Virtual Disk...`.
        - Chọn Pool.
        - Đặt tên cho Virtual Disk (ví dụ: `UserDataDisk`).
        - **Giải thích các loại Resiliency (Layout):**
            - **Simple:** (Tương tự RAID 0) Ghi dữ liệu tuần tự lên các đĩa. Hiệu năng cao nhất nhưng **không có khả năng chịu lỗi**. Một đĩa hỏng là mất hết dữ liệu. Dung lượng sử dụng bằng tổng dung lượng các đĩa.
            - **Mirror:** (Tương tự RAID 1) Ghi dữ liệu giống hệt nhau lên 2 hoặc 3 đĩa. **Khả năng chịu lỗi cao**, hiệu năng đọc tốt. Dung lượng sử dụng bằng 1/2 (two-way mirror) hoặc 1/3 (three-way mirror) tổng dung lượng. Yêu cầu ít nhất 2 đĩa.
            - **Parity:** (Tương tự RAID 5) Ghi dữ liệu và thông tin chẵn lẻ (parity) lên các đĩa. **Vừa tiết kiệm dung lượng, vừa có khả năng chịu lỗi** (chịu được 1 đĩa hỏng). Hiệu năng ghi chậm hơn Mirror. Dung lượng sử dụng = (Tổng dung lượng) - (Dung lượng 1 đĩa). Yêu cầu ít nhất 3 đĩa.
        - **Lựa chọn:** Với 3 đĩa, **Parity** là lựa chọn tốt để chứng minh kiến thức về khả năng chịu lỗi và hiệu quả dung lượng. Nếu muốn hiệu năng cao hơn, có thể chọn **Two-way mirror** (sẽ chỉ dùng 2 trong 3 đĩa). Ta sẽ chọn **Parity**.
        - **Provisioning Type:**
            - **Thin:** Cấp phát dung lượng ảo. Ổ đĩa sẽ chỉ chiếm dụng không gian vật lý khi dữ liệu được ghi vào. Linh hoạt nhưng cần theo dõi.
            - **Fixed:** Cấp phát toàn bộ dung lượng ngay từ đầu. Hiệu năng tốt hơn.
            - Chọn **Thin**.
        - Chỉ định dung lượng cho Virtual Disk (ví dụ: 18GB).
            
            ![image.png](/image/image%2057.png)
            
    5. **Tạo Volume:**
        - Sau khi tạo Virtual Disk, wizard tạo Volume sẽ tự động chạy.
        - Chọn server và disk.
        - Chỉ định dung lượng cho Volume (có thể dùng toàn bộ).
        - Chọn ký tự cho ổ đĩa (ví dụ: P:).
        - **File System Settings:** Chọn **NTFS** (phổ biến) hoặc **ReFS** (Resilient File System - mạnh mẽ hơn cho ảo hóa và dữ liệu lớn). Chọn NTFS.
        - Đặt tên cho Volume Label (ví dụ: `SharedData`).
        - Hoàn tất wizard.
            
            ![image.png](/image/image%2058.png)
            
            ![image.png](/image/image%2059.png)
            
            ![image.png](/image/image%2060.png)
            
    [![Video triển khai Windows Server](images/Picture1.gif)](https://youtube.com/playlist?list=PL8Q9o0_e7O9J0CwLQAX461xbGtEV9lKE1&si=ZgIEgWzmTCCGPWo8)
    ---