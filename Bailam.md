# Tìm hiểu về http
---
Thực hiện: **Phạm Văn Đạt**

## Mục lục   
[1. HTTP là gì?](#1)         
[2. HTTP - Các tham số](#2)          
[3. HTTP - Thông báo(Message)](#3)             
[4. HTTP - Yêu cầu(Request)](#4)            
[5. HTTP - Phản hồi(Response)](#5)                
[6. HTTP - Phương thức(Method)](#6)           
[7. HTTP - Mã hóa trạng thái](#7)            
[8. HTTP - Các trường Header](#8)             
[9. HTTP - Caching](#9)            
[10. Mã hóa URL](#10)             
[11. Bảo mật](#11)            
[12. Ví dụ về Massage](#12)  
           
---
# Nội dung

<a name="1"></a>
## 1. HTTP là gì?
* HTTP là một giao thức cấp độ ứng dụng cho các hệ thống thông tin phân phối, cộng tác, đa phương tiện. Đây là nền tảng cho giao tiếp dữ liệu cho WWW (ví dụ: Internet) từ 1990.
* HTTP là giao thức chung và stateless mà có thể được sử dụng cho các mục đích khác cũng như các sự co dãn của các phương thức được yêu cầu, các code lỗi và Hesder của nó.
* HTTP là một giao thức giao tiếp trên cơ sở TCP/IP, mà được sử dụng phân phối dữ liệu(các tệp HTML, các file ảnh,..) trên www, Cổng mặng định là TCP 80. 
* Chi tiết kỹ thuật HTTP xác định cách mà dữ liệu yêu cầu của Client sẽ được xây dựng và được gửi tới Server, và cách để server phản hồi các yêu cầu này.

- **Các đặc trưng cơ bản**
 * Có 3 đặc trưng cơ bản:
      * **HTTP là giao thức connectionless(kết nối không liên tục)**: Client của HTTP. Là Client tạo 1 yêu cầu HTTP gửi tới Server và ngắt kết nối từ Client tới Server và đợi cho 1 phản hồi, sau đó Server sử lý yeu caaif và gưi lại phản hồi cho Client.
      * **HTTP là một phuong tiện đọc lập**: Bất kỳ dữ liệu nào cũng có thẻ gửi được bởi HTTP miễn alf Server và Client biết cách kiểm soát được nội dung dữ liệu. Yêu cầu Server và Client sử dụng kiểu MIME thích hợp để xác dịnhđược kiểu nội dung.
      * **HTTP là stateless**: HTTP là connectionless nên kết quả là HTTP trở thành một giao thức Stateless. Server và Client chỉ biết nhau tại thời điểm có yêu cầu hiện tại, sau đó cả hai sẽ quên nau luôn. Do bản chất của giao thức, cả Client và các trình duyệt có thể giữ lại thông tin giữa các yêu cầu khác nhau giữa các trang web.

- **Cấu trúc cơ bản**
 * Sơ đồ biểu hiện cấu trúc đơn giản của một ứng dụng Web và miêu tả vị trí của HTTP:
 <img src="http://imageshack.com/a/img923/5160/VC8oSU.png"/>   

 * Giao thức HTTP là giao thức yêu cầu/phản hồi dự trên cấu trúc server/client, nơi mà các trình duyệt Web, các thiết bị tìm kiếm,... hoạt động như các client, và các server web hoạt động như server.
 * **Client**: Gửi yêu cầu tới Server theo mẫu cảu một phương thức yêu cầu, ỦI, và phiên bản giao thức, được theo bởi một thông báo MIME chứa các bộ chỉnh sửa yêu cầu, thông tin Client và nội dung có thể qua một kết nối TCP/IP.
 * **Server**: Phản hồi vói một dòng trạng thái, bao gồm phiên bản giao thức của thông báo và môt code thành công hoặc lỗi, theo sau bởi mỗi thông báo MIME chứa thông tin server, thông tin thực thể đa phuong tiện và nội dung đối tượng có thể.

<a name="2"></a>
## 2. HTTP - Các tham số

**- Phiên bản HTTP** 

 * HTTP sử dụng một sơ đồ đánh số `<major>.<minor>` để chỉ phiên bản của giao thức. Phiên bản của một thông báo HTTP được chỉ bởi một trường HTTP-Version trong dòng đầu tiên. Tại đây là cú pháp chung của việc xác định số phiên bản HTTP:  
`HTTP-Version ="HTTP" "/" 1*DIGIT "." 1*DIGIT`

ví dụ:
```
      HTTP/1.0
      or
      HTTP/1.1
```

**- Uniform Resource Identifiers - Bộ nhận diện nguồn tài nguyên đồng nhất**   
 * URI là một định dạng tài nguyên thống nhất (URI, viết tắt từ Uniform Resource Identifier) là một chuỗi ký tự được sử dụng để xác định, nhận dạng một tên hoặc một tài nguyên. Việc xác định như vậy cho phép tương tác với các thể hiện tài nguyên trên mạng (thường là World Wide Web) sử dụng các giao thức cụ thể.
 * Ví dụ:   
` URI="http:" "//" host [ ":" port ] [abs_path ["?" query]] `
 * Với: * **port** để trống thì tự hiểu là port 80
        * **abs_path** tương đương vs 1 "/".
        * **reserved** và **unsafe** tương đương với mã hóa "%" "HEX HEX" tương ứng.
 * Ví dụ các URI tương ứng
```
  http://abc.com:80/~smith/home.html
  http://ABC.com/%7Esmith/home.html
  http://ABC.com:/%7esmith/home.html
```

**- Các định dạng Ngày/Thời gian**  
 * Tất cả các nhãn Ngày/Thời gian HTTP Phải được biểu diễn trong Greenwich Mean Time (GMT), không có sự ngoại trừ. Các ứng dụng HTTP được cho phép để sử dụng 3 nhãn đại diện Ngày/Thời gian sau:
```
 Sun, 06 Nov 1994 08:49:37 GMT  ; RFC 822, updated by RFC 1123
 Sunday, 06-Nov-94 08:49:37 GMT ; RFC 850, obsoleted by RFC 1036
 Sun Nov  6 08:49:37 1994       ; ANSI C's asctime() format
```

**- Các bộ ký tự**   
 * Chúng ta sử dụng các bộ ký tự để xác định các thiết lập ký tự mà Client ưa thích. Nhiều bộ thiết lập ký tự có thể được liệt kê riêng biệt bởi các dấu phảy. Nếu một giá trị là không được xác định, mặc định là US-ASII.
 * Ví dụ:
```
 US-ASCII

 or

 ISO-8859-1

 or 

 ISO-8859-7
```

**- Mã hóa nội dung**   
 * Là một thuật toán mã hóa đã được sử dụng để mã hóa nooin dung trước khi nó được truyền đi. Mã háo nội dung được dùng để nén dữ liệu để cho thông tin được nhẹ hơn và chuyền tải giễ dàng hơn hoặc làm cho thông tin hoàn thiện và đảm bảo hơn trước khi truyền đi mà không bị thất lạc nhận diện.
 * Tất cả các giá trị mã hóa nội dung là không phân biệt kiểu chữ (case-insensitive). HTTP/1.1 sử dụng các giá trị mã hóa nội dung trong các trường Accept-Encoding và Content-Encoding Header mà chúng ta sẽ quan sát trong các chương kế tiếp.
 * Ví dụ: sơ đồ mã hóa hợp lệ
```
 Accept-encoding: gzip

 or

 Accept-encoding: compress

 or 

 Accept-encoding: deflate
```

**- Các kiểu đa phương tiện (media types)**   
 * HTTP sử dụng các Kiểu phương tiện Internet trong các trường **Content-Type** và **Accept** để cung cấp dữ liệu mở và có thể mở rộng. Tất cả các giá trị kiểu phương tiện được đăng ký với IANA (Internet Assigned Number Authority). Cú pháp chung để xác định kiểu phương tiện như sau:
```
 media-type     = type "/" subtype *( ";" parameter )
```
 Các thuộc tính type, subtype và parameter là case-insentive 
 * Ví dụ:
`Accept: image/gif`

**- Các thẻ ngôn ngữ**   
 * HTTP sử dụng các thẻ ngôn ngữ trong các trường Accept-Language và Content-Language. Một thẻ ngôn ngữ bao gồm một hoặc nhiều phần: Một thẻ ngôn ngữ sơ cấp và một dãy các thẻ phụ:
`language-tag  = primary-tag *( "-" subtag )` 
 Các khoảng trắng không được cho phép trong thẻ và tất cả các thẻ là case-insentive.
 * Ví dụ: Các thẻ ví dụ bao gồm:
```
 en, en-US, en-cockney, i-cherokee, x-pig-latin
```
 * Hai chữ primary-tag là một chữ viết tắt cho ngôn ngữ trong ISO-639 và hai ký tự đầu tiên trong thẻ phụ subtag là mã quốc gia.


<a name="3"></a>
## 3. HTTP - Thông báo(Message)
* HTTP được xây dựng trên cơ sở mô hình Client-Server và giao thức Stateless các yêu cầu/phản hồi được trao đổi các thông báo(Message) dọc theo một lết nối TCP/IP
* Một Client là một chương trình mà thiết lập một kết nối tới một Server cho mục đích gửi một hoặc nhiều thông báo yêu cầu HTTP. Một HTTP Server là một chương trình mà chấp nhận các kết nối để phụ vụ các yêu cầu HTTP bởi việc gửi các thông báo phản hồi HTTP.
* HTTP sử dụng URI để nhận diện một nguồn đã cho và để thiết lập một kết nối. Một khi một kết nối được thiết lập, các thông báo HTTP được truyền trong một định dạng.ác thông báo này bao gồm các Yêu cầu từ Client tới Server và các Phản hồi từ Server tới Client  mà sẽ theo định dạng sau:
```
 HTTP-message   = <Request> | <Response> ; HTTP/1.1 messages
```
* Các yêu cầu và phản hồi HTTP sử dụng 1 định dạng thông báo chung của RFC 822 cho chuyền tải dữ liệu đưuọc yêu cầu. Định bạng thông báo chung này gốm 4 phần:
```
 Một dòng đầu tiên

 Không hoặc nhiều trường Header theo sau bởi CRLF.

 Một dòng trống (ví dụ: một dòng mà không có gì trước CRLF), chỉ phần cuối của trường Header. 

 Một thân thông báo tùy ý

 ```
 * Dòng đầu thông báo(Start-line)
      * Một dòng đầu sẽ có cú pháp chung như sau:
     ```
      start-line = Request-Line | Status-Line
     ```
      * 
      * Trong đó **Request-Line** là yêu cầu của client còn **Status-Line** là phản hồi của server. Ví dụ:
     ```
      GET /hello.jsp HTTP/1.1     (This is Request-Line sent by the client)

      HTTP/1.1 200 OK             (This is Status-Line sent by the server)
     ```
 * Các trường Header
      * Các trường Header cung cấp thông tin được yêu cầu về yêu cầu hoặc phản hồi, hoặc về đối tượng được gửi trong thân thông báo.
      * Có 4 kiểu của Header trong các thông báo HTTP:  
           * Kiểu chung (General-Header): Các trường Header này có khả năng ứng dụng chung cho cả các thông báo yêu cầu và phản hồi.
           * Kiểu yêu cầu (Request-Header): Các trường Header này chỉ có khả năng áp dụng cho các thông báo yêu cầu.
           * Kiểu phản hồi (Response-Header): Các trường Header này chỉ có khả năng áp dụng cho các thông báo phản hồi.
           * Kiểu thực thể (Entity-Header): Các trường này xác định thông tin về thân-thực thể hoặc, nếu không có phần thân nào hiển thị, về nguồn được nhận diện bởi yêu cầu.
      * Tất cả các header ở trên đều được định dạng chung theo một định dạng chung là tên được theo bởi một dấu ":". Ví dụ:
     ```
      message-header = field-name ":" [ field-value ]
     ```
      * Một số Header đa dạng:
     ```
      User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
      Host: www.example.com
      Accept-Language: en, mi
      Date: Mon, 27 Jul 2009 12:28:53 GMT
      Server: Apache
      Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
      ETag: "34aa387-d-1568eb00"
      Accept-Ranges: bytes
      Content-Length: 51
      Vary: Accept-Encoding
      Content-Type: text/plain
     ```
 * Phần thân thông báo
      * Phần thân thông báo là tùy ý cho một thông báo HTTP nhưng nếu nó là có sẵn, thì khi đó nó được sử dụng để mang phần thân được liên kết với yêu cầu hoặc phản hồi. Nếu phần thân thực thể được liên kết, thì sau đó thường các dòng Content-Type và Content-Length xác định bản chất của phần thân được liên kết.
      * Một phần thân thông báo là phần mà mang dữ liệu yêu cầu HTTP thực sự (bao gồm dữ liệu mẫu và được tải lên,…) và dữ liệu phản hồi HTTP từ Server (bao gồm các file, ảnh, …). Dưới đây là nội dung đơn giản của một phần thân thông báo:
     ```
      <html>
           <body>
   
                <h1>Hello, World!</h1>
   
           </body>
      </html>
     ```    

<a name="4"></a>
## 4. HTTP - Yêu cầu(Request)
* Một Client gửi một yêu cầu HTTP tới một Server trong mẫu một thông báo yêu cầu mà bao gồm định dạng sau:
```
 Một dòng yêu cầu

 Không hoặc nhiều hơn trường Header (General|Request|Entity) được theo sau bởi CRLF.

 Một dòng trống (ví dụ: một dòng không có gì đằng trước CRLF) chỉ phần kết thúc của trường Header.

 Một phần thân thông báo tùy ý
```
* **Dòng yêu cầu:**
 * Dòng yêu cầu bắt đầu với một thủ tục method, được theo sau bởi một Reqeust-URI đã cung cấp. Method là case-intensive và nên luôn luôn được dề cập trong chữ hoa. 
 * Bảng sau liệt kê tất cả các Method đưuọc hỗ trợ trong HTTP/1.1

|STT| Phương thức và Miêu tả |
|---|------------------------|
|1|**Get**: Lấy một tài nguyên hiện có. URL chứa tất cả các thông tin cần thiết mà máy chủ cần để định vị và trả lại tài nguyên|
|2|**HEAD**: Tương tự như GET, nhưng nó truyền tải dòng trạng thái và khu vực Header.|
|3|**POST**: Tạo một tài nguyên mới. Yêu cầu POST thường mang theo một payload xác định dữ liệu cho tài nguyên mới.|
|4|**PUT**: Thay đổi tất cả các đại diện hiện tại của nguồn mục tiêu với nội dung được tải lên.|
|5|**DELETE**: Gỡ bỏ tất cả các đại diện hiện tại của nguồn mục tiêu bởi URI.|
|6|**CONNECT**: Thiết lập một tunnel tới Server được xác định bởi URI đã cung cấp.|
|7|**OPTIONS**: Miêu tả các chức năng giao tiếp cho nguồn mục tiêu.|
|8|**TRACE**: Trình bày một vòng lặp kiểm tra thông báo song song với path tới nguồn mục tiêu. |
* **Request-URI**
 * Là một Bộ nhận diện Nguồn Đồng nhất (URI) và xác định nguồn mà áp dụng yêu cầu
 * Các mẫu dùng để sác định một URI
```
 Request -URI = "*" | absoluteURI | abs_path | authority
```
|STT| Phương thức miêu tả |
|---|---------------------|
|1| Một dấu * được sử dụng khi một yêu cầu HTTP không áp dụng tới một nguồn cụ thể, nhưng tới chính Server đó. Ví dụ: `OPTIONS * HTTP/1.1`|
|2| **absoluteURI** được sử dụng khi một yêu cầu HTTP đang được tạo ra cho một suwk ủy nhiệm. Sựu ủy nhiệm được yêu cầu chuyển tới yêu cầu hoạch dịnh vụ từ một cache hiệu lực, và trả lại phản hồi. Ví dụ:`GET http://www.w3.org/pub/WWW/TheProject.html HTTP/1.1`|
|3|  Mẫu phổ biến nhất của Request-URI được sử dụng để xác định một nguồn trên một Server hoặc gateway ban đầu. Ví dụ, một Client mong muốn lấy được một nguồn một cách trực tiếp từ Server ban đầu sẽ tạo một kết nối TCP tới port 80 của host `www.w3.org` và gửi các dòng sau:`GET /pub/WWW/TheProject.html HTTP/1.1` và `Host: www.w3.org`. Ghi chú rằng, đường truyền tuyệt đối không thể là trống rỗng; nếu không gì được trình bày trong URI ban đầu, nó Phải được cung cấp như là "/" (Server root).|

* **Các trường Header Yêu cầu**
 * Các trường Request-Header cho phép Client truyền thông tin thêm về yêu cầu, và về chính client đó tới Server. 
 * Một số trường Request-Header quan trọng:
      * Accept-charset 
      * Accept-Encoding
      * Accept-Language
      * Authorization
      * Expect 
      * From
      * Host
      * If-Match
      * If-Modified-Since
      * If-Modified-Since
      * If-Range
      * If-Unmodified-Since
      * Max-Forwards
      * Proxy-Authorization
      * Range
      * Referer
      * TE
      * User-Agent
* **Các ví dụ của Thông báo Yêu cầu**
  * Tạo một yêu cầu HTTP đến địa chỉ trang **hello.htm** từ Server chạy đến tutorialspoint.com.
```
 GET /hello.htm HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Accept-Language: en-us
 Accept-Encoding: gzip, deflate
 Connection: Keep-Alive
```
 * Tại đây chúng ta không gửi bất cứ yêu cầu dữ liệu tới Server bởi vì chúng ta đang chỉ thị một trang thuần HTML từ Server. Kết nối là General-Header, và phần còn lại của Header là các Header yêu cầu. Ví dụ sau đây chỉ cách để gửi dữ liệu mẫu tới Server bởi sử dụng phần thân thông báo yêu cầu:
```
 POST /cgi-bin/process.cgi HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Content-Type: application/x-www-form-urlencoded
 Content-Length: length
 Accept-Language: en-us
 Accept-Encoding: gzip, deflate
 Connection: Keep-Alive
 
 licenseID=string&content=string&/paramsXML=string
```
 * Ở đây, URl được cung cấp /cgi-bin/process.cgi sẽ được sử dụng để xử lý dữ liệu được truyền và theo đó, một phản hồi sẽ được trả lại. Ở đây content-type nói cho Server rằng dữ liệu được truyền là một dữ liệu mẫu web đơn giản và length sẽ là độ dài thực của dự liệu đặt trong phần thân thông báo. Ví dụ sau chỉ cách bạn có thể truyền XML thuần tới Server của bạn
```
 POST /cgi-bin/process.cgi HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Content-Type: text/xml; charset=utf-8
 Content-Length: length
 Accept-Language: en-us
 Accept-Encoding: gzip, deflate
 Connection: Keep-Alive

 <?xml version="1.0" encoding="utf-8"?>
 <string xmlns="http://clearforest.com/">string</string>
```

<a name="5"></a>
## 5. HTTP - Phản hồi(Response)
* Sau khi nhận và phiên dịch một thông báo yêu cầu, một Server gửi tín hiệu phản hồi với một thông báo phản hồi HTTP.
```
 Một dòng trạng thái (Status-Line)

 Không hoặc nhiều hơn trường Header (General|Response|Entity) được theo sau bởi CRLF.

 Một dòng trống (ví dụ: một dòng không có gì đằng trước CRLF) chỉ phần kết thúc của trường Header.

 Một phần thân thông báo tùy ý
```
* **Dòng trạng thái**
 * Một dòng trạng thái bao gồm phiên bản giao thức được theo sau bởi một mã hóa trạng thái số và cụm từ thuần văn bản được liên kết của nó.
``` 
 Status-Line = HTTP-Version SP Status-Code SP Reason-Phrase CRLF
```
* **Phiên bản HTTP**
 * Một Server hỗ trợ phiên bản HTTP/1.1 sẽ trả lại thông tin phiên bản như sau
```
 HTTP-Version = HTTP/1.1
```
* **Mã hóa trạng thái** 
 * Yếu tố Status-Code là một số nguyên 3 ký tự, trong đó ký tự đầu tiên của mã hóa trạng thái định nghĩa hạng (loại) phản hồi và hai ký tự cuối không có bất cứ vai trò phân loại nào. Có 5 giá trị của ký tự đầu tiên:

|STT| Phương thức miêu tả |
|---|---------------------|
|1| **1xx: Thông tin**: Nó nghĩa là yêu cầu đã được nhận và tiến trình đang tiếp tục.|
|2| **2xx: Thành công**: Nó nghĩa là hoạt động đã được nhận, được hiểu, và được chấp nhận một cách thành công.|
|3| **3xx: Sự điều hướng lại**: Nó nghĩa là hoạt động phải được thực hiện để hoàn thành yêu cầu.|
|4| **4XX: Lỗi Client**: Nó nghĩa là yêu cầu chứa cú pháp không chính xác hoặc không được thực hiện.|
|5| **5xx: Lỗi Server**: Nó nghĩa là Server thất bại với việc thực hiện một yêu cầu nhìn như có vẻ khả thi.|
* **Các trường Header Phản hồi**
 * Các trường Header phản hồi cho phép Server truyền thông tin thêm về phản hồi mà không thể được đặt trong dòng Status-Line. Những trường Header này cung cấp thông tin về Server và về truy cập từ xa tới nguồn được xác định bởi Request-URI.
      * Accept-Ranges
      * Age
      * ETag
      * Location
      * Proxy-Authenticate 
      * Retry-After
      * Server
      * Vary
      * WWW-Authenticate
* **Các ví dụ về Thông báo Phản hồi**
 * Tạo một phản hồi HTTP cho một yêu cầu để chỉ thị trang hello.jsp từ Server đang chạy trên tutorialspoint.com.
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
 Content-Length: 88
 Content-Type: text/html
 Connection: Closed
```
```
 <html>
      <body>
           <h1>Hello, World!</h1>
      </body>
 </html>
```
 * Ví dụ sau đây chỉ một thông báo phản hồi HTTP hiển thị trạng thái lỗi khi Server không thể tìm thấy trang được yêu cầu:
```
 HTTP/1.1 404 Not Found
 Date: Sun, 18 Oct 2012 10:36:20 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 230
 Connection: Closed
 Content-Type: text/html; charset=iso-8859-1
```
```
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html>
 <head>
      <title>404 Not Found</title>
 </head>
 <body>
      <h1>Not Found</h1>
      <p>The requested URL /t.html was not found on this server.</p>
 </body>
 </html>
```
 * Tiếp theo là một ví dụ của một thông báo phản hồi HTTP chỉ trạng thái lỗi khi Server nhập vào một phiên bản HTTP sai trong yêu cầu HTTP đã cung cấp:
```
 HTTP/1.1 400 Bad Request
 Date: Sun, 18 Oct 2012 10:36:20 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 230
 Content-Type: text/html; charset=iso-8859-1
 Connection: Closed
```
```
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html>
 <head>
      <title>400 Bad Request</title>
 </head>
 <body>
      <h1>Bad Request</h1>
      <p>Your browser sent a request that this server could not understand.</p>
      <p>The request line contained invalid characters following the protocol string.</p>
 </body>
 </html>
```

<a name="6"></a>
## 6. HTTP - Phương thức(Method)
* **Phương thức GET**
 * Một yêu cầu Get lấy dữ liệu từ một Server bởi việc xác định các tha số trong đoạn URI cảu yêu cầu. Đây là phương thức chính được thực hiện để thu hồi dữ liệu.
 * Ví dụ: dùng phương thức Get để chỉ thị *hello.htm*.
```
 GET /hello.htm HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Accept-Language: en-us
 Accept-Encoding: gzip, deflate
 Connection: Keep-Alive
```
 * Server sẽ phản hồi lại yêu cầu trên là như sau:
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
 ETag: "34aa387-d-1568eb00"
 Vary: Authorization,Accept
 Accept-Ranges: bytes
 Content-Length: 88
 Content-Type: text/html
 Connection: Closed
```
```
 <html>
 <body>
 <h1>Hello, World!</h1>
 </body>
 </html>
```
* **Phương thức HEAD**
 * Phương thức Head có chức năng tương tự Get, ngoại trừ là Server phản hồi với một dòng các Hearder phản hồi, nhưng không có phần thân dối tượng.
 * Ví dụ: Cách sử dụng phương thức Head để chỉ thị thông tin Header về *hello.htm*.
```
 HEAD /hello.htm HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Accept-Language: en-us
 Accept-Encoding: gzip, deflate
 Connection: Keep-Alive
```
 * Server phản hồi lại yêu cầu HEAD trên như sau:
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
 ETag: "34aa387-d-1568eb00"
 Vary: Authorization,Accept
 Accept-Ranges: bytes
 Content-Length: 88
 Content-Type: text/html
 Connection: Closed
```

 *Bạn chú ý rằng tai đây Server không gửi bất cứ dữ liệu nào sau Header.*

* **Phương thức POST**
 * Được suwer dụng khi bạn gửi một vài dữ liệu tới Server, như cập nhập file, dữu liệu mẫu,...
 * Ví dụ: Sử dụng phương thức POST để gửi một dữ liệu mẫu tới Server, mẫu đó được sử lý bởi một *process.cgi* và sễ được trả lại phản hồi.
```
 POST /cgi-bin/process.cgi HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Content-Type: text/xml; charset=utf-8
 Content-Length: 88
 Accept-Language: en-us
  Accept-Encoding: gzip, deflate
 Connection: Keep-Alive
```
```
 <?xml version="1.0" encoding="utf-8"?>
 <string xmlns="http://clearforest.com/">string</string>
```
* Bên Server, scipt *process.cgi* xử lý dữ liệu đã truyền và gửi phản hồi như sau:
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
 ETag: "34aa387-d-1568eb00"
 Vary: Authorization,Accept
 Accept-Ranges: bytes
 Content-Length: 88
 Content-Type: text/html
 Connection: Closed
```
```
 <html>
 <body>
 <h1>Request Processed Successfully</h1>
 </body>
 </html>
```
* **Phương thức PUT**
 * Sử dụng để yêu cầu Server lưu dữ phân thân dối tượng được bao gồm tại một vị trí được xác định bởi URL đã cung cấp.
 * Ví dụ: Yêu cầu Server lưu phần thân đối tượng đã cấp trong *hello.htm* tại **root** của server.
```
 PUT /hello.htm HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Accept-Language: en-us
 Connection: Keep-Alive
 Content-type: text/html
 Content-Length: 182
```
```
 <html>
 <body>
 <h1>Hello, World!</h1>
 </body>
 </html>
```
* Server sẽ lưu phần thân đối tượng trong tệp *hello.jsp* và sẽ gửi phản hồi sau trở lại Client:
```
 HTTP/1.1 201 Created
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Content-type: text/html
 Content-length: 30
 Connection: Closed
```
```
 <html>
 <body>
 <h1>The file was created.</h1>
 </body>
 </html>
```  
* **Phương thức DELETE**
 * Dùng để yêu cầu Server xóa một file tại vị trí sác định bởi URL cung cấp. 
 * Ví dụ: Xóa tệp tin *hello.htm* tại **root** của server.
```
 DELETE /hello.htm HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
 Host: www.tutorialspoint.com
 Accept-Language: en-us
 Connection: Keep-Alive
```
* Server sẽ xóa một tệp đã được đề cập và sẽ gửi phản hồi trở lại tới Client:
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Content-type: text/html
 Content-length: 30
 Connection: Closed
```
```
 <html>
 <body>
 <h1>URL deleted.</h1>
 </body>
 </html>
```
* **Phương thức CONNECT**
 * Sử dụng Client để tạo thành một liên kết với Server qua HTTP.
 * Ví dụ: Yêu cầu một kết nối với một Server đang chạy trên host *tutorialsponit.com*
```
 CONNECT www.tutorialspoint.com HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
```
* Kết nối được thành lập với Server và phản hồi sau được gửi trả lại tới Client:
```
 HTTP/1.1 200 Connection established
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
```
* **Phương thức OPTIONS**
 * Sử dụng bởi Client để tìm các phương thức HTTP có các chức năng hỗ trợ bởi Server. Client có thể xác định một URL có phương thức Options hoặc một dấu * đẻ hướng dẫn tới toàn bộ Server.
 * ví dụ: yêu cầu một danh sách, các phương thức hỗ trợ Server chạy trên *tutorialpoint.com*
```
 OPTIONS * HTTP/1.1
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
```
* Server sẽ gửi một thông tin dựa trên định cấu hình hiện tại của Server,
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Allow: GET,HEAD,POST,OPTIONS,TRACE
 Content-Type: httpd/unix-directory
```
* **Phương thức TRACE**
 * Sử dụng để ánh sạ các nội dung cảu một yêu cầu HTTP tới ng yêu cầu mà có thể sử dụng cho mục đích *debug* tại thời điểm của sự phát triển.
 * Ví dụ: 
```
 TRACE / HTTP/1.1
 Host: www.tutorialspoint.com
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
```
* Server sẽ gửi thông báo sau trong phản hồi tới yêu cầu trên
```
 HTTP/1.1 200 OK
 Date: Mon, 27 Jul 2009 12:28:53 GMT
 Server: Apache/2.2.14 (Win32)
 Connection: close
 Content-Type: message/http
 Content-Length: 39

 TRACE / HTTP/1.1
 Host: www.tutorialspoint.com
 User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
```

<a name="7"></a>
## 7. HTTP - Mã hóa trạng thái
**1xx: Thông tin**

| Thông báo | Miêu tả |
|-----------|---------|
| 100 continue| Chỉ một phần yêu cầu được nhận bởi Server, nhưng miễn là nó không bị loại bỏ, Client nên tiếp tục với yêu cầu|
| 101 Switching  Protoconl| Server chuyển đổi giao thức|

**2xx: Thành công**

| Thông báo | Miêu tả |
|-----------|---------|
| 200 OK | Yêu cầu là OK|
| 201 Created | Yêu cầu là hoàn thành, và mở nguồn mới được tạo|
| 202 Acceted | Yêu cầu được chấp nhận cho sử lý, nhưng việc sử lý chưa hườn thành|
| 203 No-authoritative information| Thông tin trong đôi tượng Header là một bảo sao nội bộ hoặc bên thứ 3 không từ Server ban đầu|
| 204 No Content| Một mã trạng thái và một Header được cung cấp trong phản hồi, nhưng không có phần thân đối tượng trong sự phản hồi|
| 205 Reset Content| Trình duyệt nên dọn sạch mẫu được sử dụng cho việc truyền tải bởi một dữ liệu đầu vào tăng thêm|
| 206 Partial Content | Server đang trả lại dữ liệu cục bộ của kích cỡ được yêu cầu. Server phải sác định dãy được bao gồm trong phản hồi với *content-Range* header.|

**3xx: Sự điều hướng lại**

| Thông báo | Miêu tả |
|-----------|---------|
| 300 Multiple choices| Một danh sách các link. Người sử dụng có thể có một link và tới vị trí đó. tối đa 5 địa chỉ|
| 301 Moved Permanently| Trang được yêu cầu di chuyển tới một URL mới|
| 302 Found | Trang được yêu cầu di chuyển tam thời đến một URL mới|
| 303 Sê other| Trang được yêu cầu có thể tìm được dưới một trang URL khác|
| 304 Not Modified| Đây là mã phẩn hòi tới một *if-modified-since* hoặc *if-none-match* header, nơi mà URL không được chỉnh sửa từ ngày cụ thể|
| 305 Use proxy | URL được yêu cầu phải truy cập thông qua một sự ủy quyền đưuọc đề cập trong *location* Header.|
| **306 Unused** | Mã này được sử dụng trong một phiên bản trước. Nó không còn được sử dụng nữa, nhưng mã này vẫn được lưu dữ|
| 307 Temporary redirect| Trang được yêu cầu đã di chuyển tới một URL mới|

**4xx: Lỗi Client**

| Thông báo | Miêu tả |
|-----------|---------|
| 400 bad request | Server không hiểu yêu cầu |
| 401 unauthorized| Trang yêu cầu cần một tên sử dụng và một mật khẩu|
| 402 payment required| ** bạn không sử dụng ma này nữa** |
| 403 Forbidden| Sự truy cập đến trang yêu cầu bị cấm|
| 404 not found| Server không thể tìm thấy trang được yêu cầu|
| 405 metod not allowed| Phương thức được xác định trogn yêu cầu là không được phép|
| 406 not acceptable| Server chỉ có thể tạo một phản hồi mà không ddowcj chấp nhận bởi Client|
| 407 Proxy authentication required| Bạn phải sác nhận với một server ủy quyền trước khi yêu cầu này được phục vụ|
| 408 request timeuot| Yêu cầu tốn thời gian nhiều hơn thời gian Server được chuẩn bị để đợi|
| 409 conflict| Yêu cầu không thể hoàn thành vì sự xung đột|
| 410 gone| Trang yêu cầu không có sẵn nữa|
| 411 Length Required|  Content-length không được xác dịnh rõ. Server sẽ không chấp nhận yếu cầu mà không có nó|
| 412 Precondition Failed| Điều kiện trước được cung cấp trong yêu cầu được tính toán là sai bởi server|
| 413 Request etity too large| Server không chấp nhận yêu cầu, bưởi vì tượng yêu cầu là quá rộng|
| 414 Request-url too long| Server không chấp nhận yêu cầu, bởi vì URL quá dài.Xảy ra khi bạn chuyển một yêu cầu "port" tới một yêu cầu Get với thông tin quá dài|
| 415 Unsupported media tupe| Server không chấp nhận yêu cầu, bởi vì kiểu phương tiện không được hỗ trợ|
| 416 Requested range not satisfiable| Dãy byte được yêu cầu là không có sẵn và beeb ngoài giới hạn|
| 417 Expecctation failed| khả năng được cung cấp trong một trường Expect không thể được kết nối bởi Server|

**5xx: Lỗi Server**

| Thông báo | Miêu tả |
|-----------|---------|
| 500 internal server error| Yêu cầu không được hoàn thành. Server bắt gặp một điều kienj không được mong đợi|
| 501 not implemented| Yêu cầu không được hoàn thành. Server hỗ trợ tính năng được yêu cầu|
| 502 bad gateway| Yêu cầu không được hoàn thành. Server nhận một phản hồi không có hiệu lức từ server ở thượng nguồn|
| 503 Server unavailable | Yêu cầu không được hoàn thành. Server tạm thời đang quá tải hoặc đang Down|
| 504 Gateway timeout| Getway bị trễ|
| 505 HTTP Version not supported| Server không hỗ trợ phiên bản giao thức http|

<a name="8"></a>
## 8. HTTP - Các trường Header
* Các trường Header cung cấp thông tin được yêu cầu về yêu cầu hoặc phản hồi, hoặc về đối tượng được gửi trong phần thân thông báo. Có 4 kiểu của trường Header thông báo HTTP:

### General Header (kiểu chung)
* Các trường Header này có khả năng ứng dụng chung cho cả các thông báo yêu cầu và phản hồi
**Trường Cache-Control**
 * Trường Header chung **Cache-Control** được sử dụng để xác định các chỉ dẫn mà PHẢI được tuân theo bởi tất cả các hệ thống bộ nhớ ẩn. Cú pháp như sau:
```
 Cache-Control : cache-request-directive|cache-response-directive
```
 * Một Client hoặc Server có thể sử dụng Header chung Cache-Control để xác định các tham số cho bộ nhớ ẩn hoặc yêu cầu các loại cụ thể của tài liệu từ bộ nhớ ẩn.
 * ví dụ:
```
 Cache-control: no-cache
```
* Một số chỉ dẫn yêu cầu bộ nhớ ẩn quan trong mà có thể sử dụng bởi **client** trong yêu cầu HTTP:

|STT| Chỉ dẫn yêu cầu bộ nhớ ẩn và miêu tả |
|---|--------------------------------------|
|1|**no-cache**: Một bộ nhứ ẩn phải không sử dụng phản hồi để làm thỏa mãn một yêu cầu theo sau mà khồng tái sác nhận thành công với Server ban đầu|
|2|**no-store**: Bộ nhớ ẩn không nên lưu dữ bất cứ thứ gì về yêu cầu Client hoặc phản hồi 
Server|
|3|**max-age = giây (s)**: Chỉ ra rằng Client đang muốn chấp nhận một mà thời gian của nó không lớn hơn thời gian đã sác định bằng giây|
|4|**max-stale [ tính bằng giây ]**: Chỉ ra rằng Client đang muốn chấp nhận một phản hồi mà đã vượt thời gian mãn hạn. Nếu số giây được cung cấp, nó phải không là hết hạn bởi nhiều hơn thời gian đó|
|5|**min-fresh = giây**: Chỉ ra răng Client đang muốn chấp nhận một phản hồi mà thời gian sống khỏe của nó là không ít hơn tuổi hiện tại của nó cộng lại với thời gian sác định bằng giây|
|6|**no-transform**: Không chuyển đổi phân thân đối tượng|
|7|**only-if-cached**: Không lấy dữ liệu mới. Bộ nhớ ẩn có thể gửi một tài liệu chỉ kho nó ở trong bộ nhớ ẩn, và không nên liên hệ với server ban đầu để xem xét nấu một bản sao mới hơn tồn tại|

* Các chỉ dẫn phản hồi bộ nhớ ẩn quan trọng sau đây có thể được sử dụng bởi **Server** trong phản hồi của nó:

|STT| Chỉ dẫn yêu cầu bộ nhớ ẩn và miêu tả |
|---|--------------------------------------|
|1|**public**: Chỉ ra rằng phản hồi có thể được giữ trong bộ nhớ ẩn bởi bất cứ bộ nhớ ẩn nào|
|2|**private**: Chỉ ra rằng tất cả hoặc một phần của thông báo phản hồi được xem như là cho một người sử dụng đơn và phải không được giữ trong bộ nhớ ẩn bởi một bộ nhớ ẩn được chia sẻ.|
|3|**no-cache**: Một bộ nhớ ẩn phải không sử dụng phản hồi để thỏa mãn một yêu cầu theo sau mà không tái xác nhận thành công với Server ban đầu.|
|4|**no-store**: Bộ nhớ ẩn không nên lưu bất cứ gì về yêu cầu Client hoặc phản hồi Server.|
|5|**no-transform**: Không chuyển đổi phần thân đối tượng.|
|6|**must-revalidate**: Bộ nhớ ẩn phải xác minh trạng thái của các tài liệu đã cũ trước khi sử dụng nó và các tài liệu đã mãn hạn không nên được sử dụng|
|7|**proxy-revalidate**: Chỉ dẫn tái xác nhận ủy quyền có cùng ý nghĩa với chỉ dẫn must-revalidate, ngoại trừ nó không áp dụng tới các bộ nhớ ẩn user agent không được chia sẻ.|
|8|**max-age = giây**: Chỉ ra rằng Client đang muốn chấp nhận một yêu cầu mà tuổi của nó không lớn hơn thời gian đã xác định bằng giây|
|9|**s-maxage = giây**: Tuổi tối đa được xác định bởi chỉ dẫn này vượt quá tuổi tối đa đã xác định bởi hoặc chỉ dẫn max-age hoặc Expires Header. Chỉ dẫn s-maxage luôn luôn được bỏ qua bởi một bộ nhớ cá nhân.|

**Trường Connection**
 * Trường Header chung Connection cho phép người gửi xác định các chức năng mà được mong ước cho kết nối cụ thể đó và phải không được giao tiếp bởi các trạm ủy quyền qua các kết nối xa hơn. 
 * Cú pháp đơn giản cho sử dụng Connection Hesder.
 * Cú pháp đơn giản đẻ sử dụng connection header
```
 Connection : "Connection"
```
* HTTP/1.1 xác định rõ chức năng kết nối **close** cho người gửi tới tín hiệu mà kết nối sẽ được đóng sau khi hoàn thành phản hồi
```
 Connection: close
```
Theo mặc định, HTTP 1.1 sử dụng các kết nối liên tục, nơi mà kết nối không tự động đóng sau khi hoàn thành một giao dịch. Trong khi đó, HTTP 1.0 không có các kết nối liên tục theo mặc định. Nếu một Client 1.0 mong muốn sử dụng các kết nối liên tục, nó sử dụng các tham số **keep-alvie** như sau:
```
 Connection: keep-alive
```

**Trường Data**
 * Tất cả các nhãn Ngày/Thời gian PHẢI được biểu diễn trong GMT. Các ứng dụng HTTP được phép sử dụng bất kỳ 3 sự bieur diễn nhãn ngày/ thời gian sau đây.
```
 Sun, 06 Nov 1994 08:49:37 GMT  ; RFC 822, updated by RFC 1123
 Sunday, 06-Nov-94 08:49:37 GMT ; RFC 850, obsoleted by RFC 1036
 Sun Nov  6 08:49:37 1994       ; ANSI C's asctime() format
```
**Trường Pragma**
 * Dùng để bao gồm các chỉ dẫn cụ thể để thực hiện mà có thể áp dụng tới bất kỳ người nhận nào trong chuỗi yêu cầu/ phản hồi.
 * Ví dụ:
```
 Pragma: no-cache
```
**Trường Trailer**
 * giá trị của trường này chỉ ra rằng thiết lập đã cho của các trường Header biểu diễn trong trailer của một thông báo được mã hóa với mã chuyển tải được đóng khối.
 * Cú pháp:
```
 Trailer : field-name
```
 * Các trường Header thông báo được liệt kê trong trường Trailer phải không bao gồm các trường Header sau:
```
 Transfer-Encoding

 Content-Length

 Trailer
```
**Trường Transfer-Encoding (Mã hóa truyền tải)**
 * trường này chỉ ra kiểu chuyền tải nào được ấp dụng tơi phần thông báo được an toàn giữa người nhận và người gửi. Không giống như **Content-encoding** bởi vì các mã hóa truyền tải là một thuộc tính của thông báo, không phải là của phần thân thông báo.
 * Cú pháp:
```
 Transfer-Encoding: chunked
```
**Trường Upgrade**
 * Trường Upgrade này cho phép Client xác định những giao thức giao tiếp thêm vào mà nó hỗ trợ và sẽ được sử dụng nếu Server tìm thấy rằng nó thích hợp để chuyển đổi giao thức.
 * ví dụ:
```
 Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11
```
**Trường Via**
 * Trường Via phải được sử dụng bởi các gateway và các trạm ủy nhiệm để chỉ ra các giao thức trung gian và người nhận
 * Ví dụ, một thông báo yêu cầu có thể được gửi từ một HTTP/1.0 User agent tới một trạm ủy nhiệm nội bộ được đặt tên mã "fred", mà sử dụng HTTP/1.1 để chuyển tiếp yêu cầu tới một trạm ủy nhiệm công cộng tại nowhere.com, mà hoàn thành yêu cầu bởi việc chuyển tiếp nó tới Server ban đầu tại www.ics.uci.edu. Yêu cầu được nhận bởi www.ics.uci.edu sẽ có trường Via như sau:
```
 Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)
```
**Trường Warning (Cảnh báo)**
 * Trường Warning được sử dụng để mang thông tin thêm về trạng thái hoặc sự truyền tải của một thông báo mà có thể không được phản ánh trong thông báo đó. Một sự phản hồi có thể mang nhiều hơn một trường Warning.
```
  Warning : warn-code SP warn-agent SP warn-text SP warn-date
```

### Request-Header (Kiểu yêu cầu)
* Các trường Hesder này có khả năng áp dụng cho các thông báo yêu cầu. 
**Trường Accept (Chấp nhận)**
 * Trường Accept này có thể được sử dụng đễ xác định các kiểu phương tiện cụ thể mà là có thể chấp nhận cho sự phản hồi.
 * Cú pháp:
```
 Accept: type/subtype [q=qvalue]
```
 * Các kiểu phương tiện có thể được liệt kê phân biệt nhau bởi các dấu phảy và giá trị q tùy ý biểu diễn một mức độ chất lượng có thể chấp nhận để chấp nhận các kiểu trên một phạm vi từ 0 tới 1.
```
Accept: text/plain; q=0.5, text/html, text/x-dvi; q=0.8, text/x-c
```
 * Đoạn này có thể được biên dịch như **text/html** và **text/x-c** và là các kiểu phương tiện được ưa thích hơn nhưng nếu chúng không tồn tại, thì sau đó gửi đối tượng **text/x-dvi** , và nếu nó không tồn tại, gửi đối tượng **text/plain**.
**Trường Accept-charset**
 * Trường này có thể được sử dụng để chỉ các bộ thiết lập ký tự nào được chấp nhạn cho sự phẩn hồi. 
 * Cú pháp:
```
 Accept-Charset: character_set [q=qvalue]
``` 
 * Nhiều bộ ký tự có thể được riêng rẽ nhau bởi các dấu phảy và giá trị **p** tùy ý biểu diễn một mức độ chất lượng có thể chấp nhận cho các bộ ký tự không được ưa thích hơn trên miền từ 0 đến 1.
```
 Accept-Charset: iso-8859-5, unicode-1-1; q=0.8
```
 * Giá trị "*" trong trường Accept-charset là mặc định bất kỳ ký tự nào cũng được chấp nhận. cho dù trong trường Accept-charset không có giá trị nào.

**Trường Accept-Encoding**
 * Trường này tương tự như Accept, nhưng hạn chế mã hóa nội dung là có thể chấp hận trong phản hồi.
 * Cú pháp:
```
 Accept-Encoding: encoding types
```
 * Ví dụ:
```
 Accept-Encoding: compress, gzip
 Accept-Encoding:
 Accept-Encoding: *
 Accept-Encoding: compress;q=0.5, gzip;q=1.0
 Accept-Encoding: gzip;q=1.0, identity; q=0.5, *;q=0
```
**Trường Accept-Language**
 * Trường này tương tự như Accept, nhưng hạn chế bố thiết lập các ngôn ngữ tự nhiên là được ưa thích hơn khi một phản hồi tới một yêu cầu.
 * Cú pháp:
```
Accept-Language: language [q=qvalue]
```
 * Các ngôn ngữ có thể phân biệt nhau bởi dấu chấm phẩy và giá trị **q** tùy ý theo mức độ chất lượng các ngôn ngữ không được ưa thích hơn trên miền 0 đến 1.
```
 Accept-Language: da, en-gb;q=0.8, en;q=0.7
```
**Trường Authorization(sử ủy quyền)**
 * Giá trị trương này bao gồm các sự ủy nhiệm mà chứa thông tin ủy quyền chủa một use agent cho phạm vi nguồn đang được yêu cầu.
 * cú pháp:
```
 Authorization : credentials
```
 * Giản đồ ủy quyền cơ bản (HTTP/1.0), tham số ủy quyền là một chuỗi của **tên sử dụng:mật khẩu** được mã hóa trong cơ sở 64 bit.
```
 Authorization: BASIC Z3Vlc3Q6Z3Vlc3QxMjM=
```
 * Giá trị trả về là: **guest:gusest123**, trong đó **guest** là tên tài khoản, **geust** là mật khẩu
**Trường Cookie**
 * Trường này chứa giá trị tên/giá trị của thông tin được lưu trong URL đó. 
 * Cú pháp:
```
 Cookie: name=value
```
 * Với nhiều Cookie thì chúng được phân cách nhau bởi dấu ";".
```
 Cookie: name1=value1;name2=value2;name3=value3
```
**Trường Expect**
 *  Trường này được sử dụng để chỉ ra rằng một bộ hành vi của Server được yêu cầu bởi Client
 * Cú pháp:
```
 Expect : 100-continue | expectation-extension
``` 
 * Nếu Server nhận được một yêu cầu mà trường Expect mà độ dãn không được hỗ trợ thì nó sẽ phẩn hồi với trạng thái 417 (sự mong đợi thất bại)
**Trường From**
 * Trường chứa địa chỉ thư điện tử để kiểm soát user agent.
 * Cú pháp:
```
 From: webmaster@w3.org
```
**Trường Host**
 * Xác định Unternet host và số hiệu cổng cảu nguồn được yêu cầu.
 * Cú pháp:
```
 Host : "Host" ":" host [ ":" port ] ;
```
 * Một host không có bất kỳ thông tin nào về port nào thì ngụ ý là port 80. hay port 80 là bort mặc định.
 * Ví dụ: yêu câu trên Server ban đầu là *http://w3.org/pub/WWW/*
```
 GET /pub/WWW/ HTTP/1.1
 Host: www.w3.org
```
**Trường If-Match** 
 * Trường if-match được sử dụng trong method đẻ làm điều kiện. Header này yêu cầu Server để biểu diễn method được yêu cầu chỉ khi giá trị được cung cấp trong thẻ này kết nối với thẻ đối tượng được cung cấp được biểu diễn bởi Etag.
```
 If-Match : entity-tag
```
 * Một dấu "*" kết nói với bất cứ đối tượng nào. hay ns cách khác thì mọi đối tượng đều được kết nối.
```
 If-Match: "xyzzy"
 If-Match: "xyzzy", "r2d2xxxx", "c3piozzzz"
 If-Match: *
```
 * Trường hợp nếu không có đối tượng nào kết nối, không có đối tượng nào hiện tại tồn tại thì server không được trình bày methor được yêu cầu và trả lại ohanr hồi 412(điều kiên trước thất bại)

**Trường  If-Modified-Since**
 * Trường này được sử dụng với một method để làm cho nó có điều kiện. Nếu URL được yêu cầu không đưuọc chỉnh sửa từ thời gian đã được xác định trong trường này, một đối tượng sẽ không đưuọc trả lại từ server thay vào đó một phản hồi 304(khong được chỉnh sửa) được trả lại và không có thêm thông báo nào. 
 * Cú pháp:
```
 If-Modified-Since : HTTP-date
```
```
 If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT
```
 * Nếu không có thẻ đối tượng nào kết nối hoặc không đối tượng hiện tại nào tôn tại thì  Server phản hồi lại  412(điều kiện trước thất bại)

**Trường If-None-Match**
 * **Tương tự trường  If-Match**
**Trường If-Range**
 * Trương Trường If-Range sử dụng 1 yêu cầu có điều kiện để chỉ một phần đối tượng nếu nó bị thất lạc hoặc toàn bộ đối tượng nếu nó được thay đổi.
 * Cú pháp:
```
 If-Range : entity-tag | HTTP-date
```
 * Để sác minh đối tượng nội bộ đã nhận một thẻ đói tượng hoặc một dữ liệu.
```
 If-Range: Sat, 29 Oct 1994 19:43:31 GMT
```
 * Tại đây, nếu tài liệu không được chỉnh sửa từ ngày đã cho, Server trả lại dãy byte được cung cấp bởi trường Range, nếu không thì nó trả lại tất cả các tài liệu mới
**Trường If-Unmodified-Since**
 * Trương này được sử dụng với một phương pháp để làm cho nó có điều kiện.
 * Cú pháp:
```
If-Unmodified-Since : HTTP-date
```
 * Nếu nguồn được yêu cầu không được chỉnh sửa từ khi thời gian đã được xác định trong trường này, Server sẻ thực hiện hoạt động được yêu cầu nếu như If-Unmodified-Since không biểu diễn
```
 If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT
```
 * Nếu yêu cầu có kết quả là bất cứ gì khác ngoài một trạng thái là 2xx hoặc 4xx, thì trường If-Unmodified-Since nên được bỏ qua.
 
**Trường Max-Forwards**





### Response-Header (Kiểu phản hồi)
* Các trường header này chỉ có khả năng áp dụng cho các thông báo phản hồi.


### Entity_Header (Kiểu thực thể)
* CÁc trường này xác định thông tin về thân-thực thể hoặc, nếu không có phần thân nào hiển thị, về nguồn được nhận diện bởi yêu cầu. 

<a name="9"></a>
## 9. HTTP - Caching

<a name="10"></a>
## 10. Mã hóa URL

<a name="11"></a>
## 11. Bảo mật

<a name="12"></a>
## 12. Ví dụ về Massage









