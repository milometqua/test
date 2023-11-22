# [JAVA] - BUỔI 5: DEV THÌ KHÔNG CHỈ VIẾT CODE
- [\[JAVA\] - BUỔI 5: DEV THÌ KHÔNG CHỈ VIẾT CODE](#java---buổi-5-dev-thì-không-chỉ-viết-code)
  - [Version Control là gì và tại sao cần dùng nó?](#version-control-là-gì-và-tại-sao-cần-dùng-nó)
  - [Các khái niệm về Git](#các-khái-niệm-về-git)
    - [Repository](#repository)
    - [Clone](#clone)
    - [Branch và Checkout](#branch-và-checkout)
    - [Commit](#commit)
    - [Pull](#pull)
    - [Push](#push)
    - [Merge](#merge)
    - [Fork](#fork)
  - [Khi nào cần Pull Request? Cách tạo Pull Request](#khi-nào-cần-pull-request-cách-tạo-pull-request)
  - [UML là gì? Lí do cần vẽ UML](#uml-là-gì-lí-do-cần-vẽ-uml)
  - [Mô hình Class Diagram](#mô-hình-class-diagram)
    - [Các thành phần của một lớp](#các-thành-phần-của-một-lớp)
  - [Mô hình Activity Diagram](#mô-hình-activity-diagram)
    - [Các thành phần của biểu đồ hoạt động](#các-thành-phần-của-biểu-đồ-hoạt-động)

## Version Control là gì và tại sao cần dùng nó?
Version control được hiểu như 1 công cụ giúp bạn theo dõi sự thay đổi của toàn bộ cấu trúc chương trình, từ các file code cho đến các file hình ảnh, video theo thời gian. Với version control, bạn có thể tạo ra nhiều phiên bản của các file ứng với từng thay đổi mà bạn tạo ra.

Nếu bạn là một nhà thiết kế đồ họa hoặc web và muốn giữ mọi phiên bản của hình ảnh hoặc bố cục (mà bạn chắc chắn muốn có nhất), Hệ thống kiểm soát phiên bản (VCS – Version Control System) là một điều rất khôn ngoan khi sử dụng. Nó cho phép bạn hoàn nguyên các tệp đã chọn về trạng thái trước đó, hoàn nguyên toàn bộ dự án về trạng thái trước đó, so sánh các thay đổi theo thời gian, xem ai đã sửa đổi lần cuối cùng điều gì đó có thể gây ra sự cố, ai đã đưa ra sự cố và khi nào, v.v. Sử dụng VCS nói chung cũng có nghĩa là nếu bạn làm hỏng mọi thứ hoặc làm mất tệp, bạn có thể dễ dàng khôi phục. Ngoài ra, bạn nhận được tất cả những điều này với chi phí rất ít.
## Các khái niệm về Git
### Repository
Là nơi lưu trữ tất cả những thông tin cần thiết để duy trì và quản lý các sửa đổi và lịch sử của dự án (nơi trữ source code và các thay đổi trên đống source code này)

Có hai loại repository:

* Local Repository: là repository nằm trên chính máy tính của chúng ta, repository này sẽ đồng bộ hóa với remote repository bằng các lệnh của git.
* Remote Repository: là repository được cài đặt trên server chuyên dụng. Ví dụ: GitHub, GitLab, Bitbucket,...

Khi tự khởi tạo một repository, chúng ta gõ lệnh `$ git init`, lệnh này sẽ tạo ra một thư mục `.git` và đây chính là repository còn phần code nằm cùng với thư mục `.git` được gọi là *Working Directory*

Sau khi gõ lệnh git init, nếu nhận được thông báo như sau thì việc thực hiện tạo repository đã thành công
> Initialized empty Git repository in path_to_folder/.git/
### Clone
Sao chép một repository có sẵn về local.
> git clone /đường-dẫn-đến-repository/

![markdown](https://images.viblo.asia/faccfa21-86ea-4fff-9313-d7f2b8407eb2.png)

Ví dụ muốn lấy source code của dự án example-project từ remote repository đặt trên Github

>$ git clone git@github.com:username/example-project.git

Nếu repository nằm ở máy chủ khác thì bạn dùng lệnh sau:

>git clone tênusername@địachỉmáychủ:/đường-dẫn-đến-repository

Trong thư mục chứa source code vừa clone sẽ có file .git và lúc này chúng ta cũng đã có một local repository
### Branch và Checkout
![markdown](https://images.viblo.asia/161b7de0-1242-4a19-95d2-4d09a75d8ae4.jpeg)

Branch là nhánh, checkout một branch nghĩa là tạo một nhánh mới từ một nhánh nào đó. Tóm lại đây là khái niệm khi dùng để phân nhánh và những thao tác sẽ được lưu trữ trên nhánh hiện tại, không làm ảnh hưởng đến nhánh cũ, như đã nói ở trên về vấn đề khi bạn muốn phát triển một tính năng mới mà đảm bảo vẫn có thể dễ dàng khôi phục lại trạng thái trước đó thì một trong những cách có thể áp dụng là tạo một branch mới và thao tác trên đó như sau:
```
$ git branch <bran-name>
```
sau đó checkout sang branch vừa tạo hoặc dùng lệnh sau để tạo branch mới và đồng checkout sang branch vừa tạo
```
$ git checkout -b <branch-name>
```
Mỗi repository có thể tạo nhiều nhánh khác nhau, và chúng độc lập với nhau nên khi bạn thực hiện các thao tác thêm xóa, cập nhật với project trên nhánh này sẽ không ảnh hưởng đến các nhánh khác. Branch mới được tạo ra sẽ chứa toàn bộ trạng thái đã thực hiện trên project ngay thời điểm trước khi được tạo.

Branch mặc định là master

Có hai loại branch:

* Local branch: nhánh nằm trên máy tính của bạn

* Remote branch: nhánh nằm trên máy chủ từ xa
### Commit
Là thao tác để lưu lại trạng thái hiện tại trên hệ thống, ghi nhận lại lịch sử các xử lý: thêm, xóa, cập nhật các file hay thư mục trên repository

Khi thực hiện, repository sẽ ghi lại sự khác biệt giữa lần commit trước so với hiện tại. Chúng được ghi nối tiếp nhau theo thứ tự thời gian. Do đó, bạn có thể xem lại lịch sử thay đổi trong quá khứ dựa theo các commit trước đó

![markdown](https://images.viblo.asia/1ecc6126-6bed-4f8f-8698-2b18e1e30ccc.jpg)

Để thực hiện một commit, bạn sử dụng lệnh sau: `$ git add .` nếu muốn lưu lại tất cả những file đã thay đổi, thêm, xóa,... hoặc `$ git add path_to_file1 path_to_file2` để lưu lại thay đổi chỉ những files mà bạn muốn

Tiếp theo chạy lệnh `$ git commit -m "Nội dung muốn commit"` để commit các thay đổi đã lưu lại ở trên.
### Pull
Là hành động cập nhật các thay đổi xuống local repo.

Ví dụ: Trong khi bạn đang code trên một file thì một người bạn trong nhóm của bạn cũng code trên một file khác cùng branch, người bạn đó hoàn thành công việc, commit và push lên remote repo. Lúc này bạn muốn lấy những thay đổi mà người bạn của bạn đã thực hiện thì bạn sẽ thực hiện hành động Pull xuống.

Vd: Cập nhật code ở branch `feature_new` ở local với từ remote thì bạn dùng lệnh sau: `$ git pull origin feature_new`. 'origin' ở đây có thể được thay thế bởi tên của remote repository
### Push
Là hành động đưa những thay đổi đã commit lên một branch nào đó ở remote repository hoặc một branch mới hoàn toàn lên remote repository. Sau khi push lên thì các thành viên của team có thể thấy và đồng bộ code xuống máy local.

Ví dụ: push một branch có tên là `new_feature` sau khi hoàn thành một feature (dĩ nhiên là đã commit) lên origin remote thì sẽ sử dụng lệnh sau: `$ git push origin new_feature`
###  Merge
Là việc hợp nhất một nhánh phát triển hoặc hợp nhất lịch sử thay đổi vào nhánh khác.

Ví dụ bạn phát triển xong 1 tính năng, đã test/kiểm tra các kiểu và thấy nó hoàn chỉnh, có thể tích hợp vào phần mềm thì bạn sẽ tiến hành merge code. Dĩ nhiên trong thực tế thì bạn đôi khi cần phải mất một vài thao tác khác như commit, push,... để có thể merge được code.
```
$ git merge <branch-name>
```
Giả sử có 2 branchs cần merge như sau:

![markdown](https://images.viblo.asia/7cdf5cf3-9f16-43cc-8a75-14d6e6890f4d.png)

Sử dụng merge sẽ có kết quả như thế này:
![markdown](https://images.viblo.asia/0410ca07-7d24-4dcf-bfdd-fa5dc6872a29.png)

Merge sẽ giữ lại lịch sử commit theo dòng thời gian.
### Fork
![markdown](https://images.viblo.asia/5380bfc7-d666-43a9-9842-c8cccf0677f0.png)

Khái niệm này trên Github, là hành động tạo một bản sao của repository gốc thành một repository của bạn. Việc fork một repository cho phép bạn dễ dàng chỉnh sửa, thay đổi source code mà không ảnh hưởng tới source gốc.

![markdown](https://images.viblo.asia/d86a5f7a-d606-4be8-9cbb-f9781824d475.png)

Nếu muốn thay đổi, bổ sung gì ở repository gốc thì bạn sẽ phải commit và push lên repository của bạn, sau đó tạo pull request để được merge vào repo chính.

Một ví dụ về việc sử dụng fork, là khi bạn muốn fix bug source code trên repository của một ai đó, khi đó bạn cần thực hiện theo quy trình sau:

1. Fork repository đó về tài khoản Github của mình
2. Thực hiện fix bug
3. Gửi một Pull Request tới repository gốc
4. Chủ sở hữu của repository nơi bạn fork sẽ review chỉnh sửa của bạn và tiến hành merge nội dung chỉnh sửa vào source gốc.
## Khi nào cần Pull Request? Cách tạo Pull Request
Pull Request là một tính năng của hệ thống quản lý mã nguồn (source control management) như Git, GitHub, hay GitLab. Nó là một cách để người dùng có thể đề xuất thay đổi vào mã nguồn của một dự án đã được lưu trữ trên hệ thống quản lý mã nguồn đó.

Khi một người dùng muốn đóng góp vào một dự án, họ có thể tạo một branch (nhánh) riêng từ branch chính (thường là branch master), thực hiện các thay đổi cần thiết trong branch này, rồi đưa các thay đổi lên remote repository và tạo một pull request. Pull request bao gồm các thông tin về các thay đổi đã thực hiện, các commit mới, các nhận xét, v.v. Người sở hữu dự án hoặc các thành viên khác của dự án có thể xem và kiểm tra các thay đổi trước khi chấp nhận hoặc từ chối pull request.

Khi một pull request được chấp nhận, các thay đổi được hợp nhất vào branch chính của dự án. Quá trình này có thể được tự động hóa bằng các công cụ tích hợp liên kết với hệ thống quản lý mã nguồn. Pull request là một cách linh hoạt và an toàn để đóng góp vào dự án và đảm bảo rằng các thay đổi mới không gây ra tác động tiêu cực đến mã nguồn hiện có.

Cách tạo Pull Request trên GitHub

Bước 1: Fork dự án gốc
* Truy cập vào dự án gốc trên GitHub.
* Nhấn vào nút “Fork” ở góc trên bên phải để sao chép dự án vào tài khoản của bạn.

Bước 2: Clone dự án về máy
* Truy cập vào repository đã fork trong tài khoản của bạn.
* Sao chép URL của repository.
* Mở Terminal và sử dụng lệnh git clone để clone dự án về máy.

Bước 3: Tạo nhánh mới
* Mở Terminal trong thư mục dự án đã clone.
* Sử dụng lệnh `git checkout -b [tên_nhánh]` để tạo và chuyển đổi sang một nhánh mới.

Bước 4: Thực hiện thay đổi
* Mở dự án trong trình chỉnh sửa mã nguồn.
* Thực hiện các thay đổi cần thiết và lưu lại.

Bước 5: Commit và Push
* Mở Terminal và sử dụng lệnh `git add .` để thêm các thay đổi vào danh sách commit.
* Sử dụng lệnh `git commit -m "Mô tả commit"` để commit các thay đổi đã thêm.
* Sử dụng lệnh `git push origin [tên_nhánh]` để đẩy thay đổi lên repository của bạn trên GitHub.

Bước 6: Tạo Pull Request
* Truy cập vào repository của bạn trên GitHub.
* Nhấn vào nút “Compare & pull request” bên cạnh tên nhánh của bạn.
* Điền thông tin cần thiết, mô tả về Pull Request và nhấn “Create Pull Request“.

Bước 7: Kiểm tra và xử lý yêu cầu chỉnh sửa
* Nhóm quản lý dự án sẽ xem xét và thảo luận về Pull Request của bạn.
* Nếu cần chỉnh sửa, bạn chỉ cần thêm commit vào nhánh đã tạo và Pull Request sẽ tự động cập nhật.

Bước 8: Pull Request được chấp nhận và merge
* Sau khi Pull Request đạt yêu cầu, nhóm quản lý sẽ chấp nhận và merge vào nhánh chính.
* Code của bạn đã được hợp nhất vào dự án gốc.
## UML là gì? Lí do cần vẽ UML
UML là một ngôn ngữ hệ thống dành cho các phần mềm và hệ thống không phải phần mềm, bao gồm các ký hiệu đồ hoạ được sử dụng để đặc tả, hình dung hay xây dựng và làm tài liệu. Nhìn chung, UML không phải là một ngôn ngữ lập trình mà là một ngôn ngữ trực quan và khá giống với các bản thiết kế của các lĩnh vực kỹ thuật khác. 

UML mang đến cơ hội để viết thiết kế hay những khái niệm, tiến trình, chức năng lên hệ thống. Nó cũng được sử dụng cho những ngôn ngữ dùng để khai báo dãy cơ sở dữ liệu, thành phần mà phần mềm có thể sử dụng lại. Ngoài ra, UML cũng đảm nhiệm vai trò thay thế các ngôn ngữ mô hình hoá điển hình như OMT, Booch, OOSE cùng với một số mô hình khác. 

Nói một cách đơn giản là nó dùng để tạo ra các bản vẽ nhằm mô tả thiết kế hệ thống. Các bản vẽ này được sử dụng để các nhóm thiết kế trao đổi với nhau cũng như dùng để thi công hệ thống (phát triển), thuyết phục khách hàng, các nhà đầu tư v.v.. (Giống như trong xây dựng người ta dùng các bản vẽ thiết kế để hướng dẫn và kiểm soát thi công, bán hàng  căn hộ v.v..)
## Mô hình Class Diagram
Một biểu đồ lớp chỉ ra cấu trúc tĩnh của các lớp trong hệ thống. Các lớp là đại diện cho các “đối tượng” được xử lý trong hệ thống. Các lớp có thể quan hệ với nhau trong nhiều dạng thức:

* liên kết (associated - được nối kết với nhau),
* phụ thuộc (dependent - một lớp này phụ thuộc vào lớp khác),
* chuyên biệt hóa (specialized - một lớp này là một kết quả chuyên biệt hóa của lớp khác),
* hay đóng gói ( packaged - hợp với nhau thành một đơn vị).

Tất cả các mối quan hệ đó đều được thể hiện trong biểu đồ lớp, đi kèm với cấu trúc bên trong của các lớp theo khái niệm thuộc tính (attribute) và thủ tục (operation). Biểu đồ được coi là biểu đồ tĩnh theo phương diện cấu trúc được miêu tả ở đây có hiệu lực tại bất kỳ thời điểm nào trong toàn bộ vòng đời hệ thống.

Một hệ thống thường sẽ có một loạt các biểu đồ lớp – không phải bao giờ tất cả các biểu đồ lớp này cũng được nhập vào một biểu đồ lớp tổng thể duy nhất – và một lớp có thể tham gia vào nhiều biểu đồ lớp.
### Các thành phần của một lớp
* Tên lớp
* Các thuộc tính
* Các phương thức

![markdown](https://images.viblo.asia/4de39b07-a41d-4e77-a2a6-b8cddd096fe8.png)
## Mô hình Activity Diagram
Biểu đồ hoạt động là biểu đồ mô tả các bước thực hiện, các hành động, các nút quyết định và điều kiện rẽ nhánh để điều khiển luồng thực hiện của hệ thống. Đối với những luồng thực thi có nhiều tiến trình chạy song song thì biểu đồ hoạt động là sự lựa chọn tối ưu cho việc thể hiện. Biểu đồ hoạt động khá giống với biểu đồ trạng thái ở tập các kí hiệu nên rất dễ gây nhầm lẫn. Khi vẽ chúng ta cần phải xác định rõ điểm khác nhau giữa hai dạng biểu đồ này là biểu đồ hoạt động tập trung mô tả các hoạt động và kết qủa thu được từ việc thay đổi trạng thái của đối tượng còn biểu đồ trạng thái chỉ mô tả tập tất cả các trạng thái của một đối tượng và những sự kiện dẫn tới sự thay đổi qua lại giữa các trạng thái đó.
### Các thành phần của biểu đồ hoạt động
* Trạng thái khởi tạo hoặc điểm bắt đầu (Initial State or Start Point)

![Markdown](https://images.viblo.asia/9ab04dff-1a3e-45bc-8679-9bd05fd2e1fd.png)

* Hoạt động hoặc trạng thái hoạt động (Activity or Action State)

![Markdown](https://images.viblo.asia/b91cefeb-85ef-4c3e-a3aa-97973a9d8dd2.png)

Hoạt động và sự chuyển đổi hoạt động được ký hiệu và cách sử dụng hoàn toàn giống như trạng thái trong biểu đồ trạng thái đã nêu ở trên.

* Nút quyết định và rẽ nhánh

Nút rẽ nhánh trong biểu đồ hoạt động được kí hiệu bằng hình thoi màu trắng.

![markdown](https://images.viblo.asia/f5396290-ffbf-4e0f-8f3f-3b1766a7d42e.png)

* Thanh tương tranh hay thanh đồng bộ

Có thể có nhiều luồng hành động được bắt đầu thực hiện hay kết thúc đồng thời trong hệ thống.

* Thanh đồng bộ kết hợp:

![markdown](https://images.viblo.asia/0e853cfb-6092-4ad2-bc80-5416df75907a.png)

* Thanh đồng bộ chia nhánh:

![markdown](https://images.viblo.asia/c518484d-ffdd-47eb-a8ac-ac0278e9ea6d.png)

* Cạnh gián đoạn (Interrupting Edge)

![markdown](https://images.viblo.asia/e9ac5753-34af-4c2c-af3b-0e85da3cf7ad.png)

* Luồng hoạt động (Action Folow)

![markdown](https://images.viblo.asia/73b5adfe-24b6-422f-a5ce-1db349134508.png)

* Phân làn (Swimlanes)

Phân làn trong biểu đồ sử dụng là những đường nét đứt thẳng đứng theo các đối tượng. Phần kí hiệu này thường được sử dụng để làm rõ luồng hoạt động của các đối tượng riêng biệt.

* Thời gian sự kiện (Time Event)

![markdown](https://images.viblo.asia/fff7c6f2-7a2f-43d8-81fd-46dc80ce7f17.png)

* Gửi và nhận tín hiệu (Sent and Received Signals)

![markdown](https://images.viblo.asia/2fe1abf6-0526-47b1-a6e4-b8c3538b8943.png)

* Trạng thái kết thúc hoặc điểm cuối (Final State or End Point)

![markdown](https://images.viblo.asia/ea5c20d0-c428-4f52-be3e-634273592671.png)

