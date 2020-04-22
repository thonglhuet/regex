Regex là pattern để match các kí tự trong 1 chuỗi kí tự.


Regex được chia ra làm nhiều flavor, mỗi flavor sẽ có một vài syntax khác nhau.

Cụ thể về Regex tại https://www.regular-expressions.info/. 

Do tài liệu tại website này khác là khó để quick-start nên mình sẽ chọn Javascript flavor đẻ tiếp cận syntax trước, sau đó sẽ qua https://www.regular-expressions.info/.

Vì là Javascript flavor nên sẽ có nhiều syntax không tồn tại hoặc khác so với các flavor khác.


## Using simple patterns

Simple pattern: Match chuỗi kí tự bình thường 
VD: QYR abc GHJ 
/abc/  -> match abc


## Flag
Regex có một số flag, nếu vào các page regex online, chúng ta có thể lúng túng khi thấy chúng
g:   global, search toàn bộ văn bản
i:   case insensitive
m:   multiline 
s:   single-line
u:   unicode
y:   sticky search


## Using special characters

### Assertions: ^, $, \b, \B

^: begining of input

```
VD: /^aT/   -> aT   baT   // match aT đầu tiên chứ k match aT thứ 2
```

$: Tương tự ^ nhưng là end of input 

\b: world-boundary

Là nhưng vị trí mà tại đó có sự chuyển giao giữa "kí tự wordword" và "kí tự không phải word"
```
VD: 

ab           -> Match  ^ và $

a de f       -> Match ^, $, 1-1, 2-2, 4-4, 5-5
```


* TH chưa giải thích được: ád   chỉ match 1-1, 2-2, không match 0-0

\B: non-word boundary

Là những vị trí không phải word-boundary
```
VD: 
ab    -> Match 1-1
abc   -> Match 1-1, 2-2
```

### Character classs

.: Tất cả các kí tự ngoại trừ xuống dòng

\d:     kí tự digit(số)

\D:     kí tự không phải số

\w      kí tự alphanumeric [A-Za-z0-9_]

\W:     kí tự không phải alphanumeric

\s:     single white space character, gồm: space, xuống dòng, tab, form-feed

\S:     các trường hợp không phải \s

\uhhhh: UTF-16 code hhhh

\:      Escape special-character




### Quantifiers

x*:   Match x 0 -> n lần    VD:    a*    Match B

x+	  Match x 1 -> n lần    VD:    a+    Match Baaaaaa

x?	  Match x 0 hoặc 1 lần 


x{n}	    Match khi x Phải xuất hiện đúng n lần

x{n,}	    Match khi x xuất hiện từ n lần trở lên

x{n,m}	  Match khi x xuất hiện trong khoảng n -> m

x*?       Mặc định thì *, + sẽ tìm số kí tự nhiều nhất có thể.  Đặt ? sau * để thành non-greddy.
```
      VD: some <foo> <bar> new </bar> </foo> thing
        /<.*>/g    -> Match  "<foo> <bar> new </bar> </foo>"
        /<.*?>/g   -> Match  "<foo>
```

Example: 
```Javascript

var wordEndingWithAs = /\w+a+/;  -> Match Spartaaaaaa
var delicateMessage = "This is Spartaaaaaaa";

```

```Javascript
var singleCharacter = /\b\w\b/g;     -> Match tất cả các từ 1 kí tự
var longCharacter = /\b\w{2,}\b/g;   -> Match tất cả các từ 2 kí tự trở lên

var sentence = "Why do I have to learn multiplication table?  1234567";

```


### Group and ranges

x|y	:     X hoặc Y 

[xyz]:    x,y hoặc z
[a-c]:    Range từ a -> c
[^xyz]:   Không nằm trong xyz
[^a-c]:   Không nằm trong range a-c
(x):      Sử dụng để nhóm các phần tử lại VD: (abc){3}
\n:       với n là number. Để Gọi capturing group thứ n từ trái sang
          VD: /ab(,)cdef\1/   match với   ab,cdef,



VD: 
```Javascript
var aliceExcerpt = "There was a long silence after this, and Alice could only hear whispers now and then.";
var regexpVowels = /[aeiouy]/g;   // Match any character inside
```




Để luyên tập, chúng ta có thể visit https://www.hackerrank.com/domains/regex