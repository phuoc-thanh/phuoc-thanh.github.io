---
layout: post
title: "Dấn thân vào nghề lập trình"
comments: true
description: "Dấn thân vào nghề lập trình"
keywords: "software, frontend, backend, developer"
---

Bài viết được dịch từ blog của Kyle Kingsbury, bài gốc tiếng Anh [ở đây](https://aphyr.com/posts/265-getting-started-in-software).

Note: Chữ in đậm là lời của người dịch (is me - Thanh P Do)

...

*Một người bạn học-đại của Tôi đang bắt đầu tự học lập trình. Anh ấy cũng hi vọng sẽ tìm được một công việc tại khu vực startup Bay Area, và anh ta có nhờ Tôi giúp đỡ định hướng. Tôi đã bắt đầu viết phản hồi, và câu trả lời đang dần trở nên rối ren. Nghĩ rằng câu trả lời này sẽ có ích với nhiều người khác (nên Kyle đăng lên blog)*.


Tôi muốn mang đến cho bạn một cái nhìn bao quát hơn về cách mà ngành công nghệ phần mềm này hoạt động - có rất nhiều tài liệu và nguồn tham khảo chi tiết hơn, cụ thể hơn, nhưng đôi khi chúng ta cũng khó mà nhìn thấy được sự tương quan giữa chúng. Có thể bạn sẽ hứng thú khi đọc lướt bài viết này trước khi chúng ta gặp nhau, khi đó những khái niệm, thuật ngữ sẽ trở nên quen thuộc hơn.

## Bằng cách nào mà Software (phần mềm) được tạo ra

Lĩnh vực phần mềm, về mặt kỹ thuật được chia làm 2 khu vực lớn, thường được biết đến với tên gọi là "development" và "operations". Phát Triển (development) là quá trình viết và tinh chỉnh phần mềm, còn Vận Hành (operations) là công việc xuất bản và triển khai/duy trì chúng. Nói chung, Tôi nghĩ rằng công việc Phát Triển thì có chút thiên về vận dụng đầu óc và ngôn ngữ hơn, còn Vận Hành thì lại thiên về kinh nghiệm xử lý và tích hợp những thành phần khác nhau.

Ngoài 2 khu vực kỹ thuật ra, thì bạn cũng có những công việc xung quanh sản phẩm và thiết kế. "Product" (Nhóm sản phẩm) chính là cách mà bạn hiểu về một vấn đề đang gặp phải, gặp những người cần giải pháp cho vấn đề đó, hiểu những công cụ mà bạn có, và mường tượng được hình hài của giải pháp tổng thể. "Design" (Nhóm thiết kế) thì lại là về cách mà giải pháp đó được diễn đạt đến con người. Tất cả mọi thứ, từ ý tưởng cốt lõi cho đến một mô hình trực quan, đến những chi tiết cụ thể nhất như màu sắc, sắp xếp, font chữ, tiếng động, hình ảnh...

Hãy tưởng tượng đến một cuộc đua xe xuyên sa mạc. Product team là nhóm lên kế hoạch tìm đường, tìm kiếm tài xế, và quyết định loại xe sẽ sử dụng. Developers sẽ thiết kế động cơ, cân bằng khí động học, tối ưu hóa chất lỏng, tính toán kích thước và xây dựng khung gầm. Designers thì sẽ định hình vẻ bề ngoài, kiểu dáng xe, chọn màu sơn, vị trí của các bộ điều khiển để tài xế có thể kiểm soát chiếc xe. Operations - đội vận hành sẽ hoạt động trên mặt đất, quan sát từ xa hiệu năng, công suất của xe, chữa cháy nếu cần thiết, thay thế thiết bị hư hỏng, hay đổi những chiếc bánh xe mới cho phù hợp với địa hình hơn.

**Như vậy là có 4 nhóm việc trong ngành IT: nhóm "Product", nhóm "Design", nhóm "Develop", nhóm "Operation"**

Designers và product team sẽ giao tiếp với nhau rất nhiều để giải quyết vấn đề, sao cho có ý nghĩa đối với người dùng. Developer và Designer làm việc chặt chẽ với nhau để định hình nên phương tiện, trong đó: designers tùy chỉnh thiết kế theo ý của người dùng, và developers tùy chỉnh thiết kế cho máy tính hiểu. Developers sẽ phản hồi với product team về những gì có thể hiện thực hóa được và product team cũng thúc giục developers giải quyết những vấn đề thực. Developers sẽ giúp đội vận hành (operations) hiểu về chiếc xe, về cách lắp ráp từng bộ phận, điểm yếu của của xe, giới hạn nhiệt, loại khí nào cần sử dụng... Đội vận hành cũng giúp developers hiểu thêm khi chiếc xe thực chạy trên đường, khi nào nó sẽ trục trặc, những bộ phận nào cần được củng cố, đâu là giới hạn tốc độ của chiếc xe...

Xây dựng nên web sites là một cách tiếp cận tốt để có thể tìm hiểu hết những vai trò kể trên. Bạn sẽ thử mỗi vai trò một ít để cảm nhận được đâu là vai trò thích hợp cho bạn.

## Thành phần của một web site

Frontend, chính là phần mà bạn nhìn thấy trên browser - trình duyệt web. Nó được cấu thành từ HTML document (một dạnh văn bản có cấu trúc), CSS stylesheet (chỉ định vị trí, màu sắc, kích cỡ của các thành phần trong website) và Javascript (giúp tạo ra sự tương tác giữa các thành phần). Những "frontend dev" sẽ đảm nhận công việc liên quan 3 thứ này HTML, CSS và Javascript, và họ thường làm việc cùng designer nữa (UI và UX).

Phần backend nằm ở server - máy chủ. Nó thường được chia nhỏ ra làm nhiều thành phần phụ. Một phần phụ trong đó sẽ `render` những chi tiết frontend và đưa nó đến với người dùng khi họ yêu cầu. Một phần khác ghi thông tin xuống database. Các thành phần còn lại sẽ đảm nhận nhiệm vụ như gọi đến dịch vụ bên thứ 3, tính toán quỹ đạo, tạo cuộc gọi thoại, v.v... Nhưng công việc này do "backend dev" đảm nhận.

Môi trường để những thứ "backend" chạy trên đó, như máy tính, hệ điều hành, dịch vụ lưu trữ, mạng, điều khiển... Mà một cô nào đó vận hành thì được gọi là "dev ops" (aka operations enginner), "netword administrator", "sysadmin" tùy theo đặc trưng riêng.

Nhiều lúc, những nhóm dev này làm việc độc lập với nhau, nhưng cũng có khi họ hoạt động sát cánh bên nhau. Một người cũng có thể đảm nhận một hoạt nhiều vai trò cùng lúc. tùy thuộc vài các tổ chức nhóm.

## Quá trình viết Code

Development is a lot like academia. Your job is to understand a problem, develop a way to talk about it, and write an argument. Just like leading a reader through a chain of reasoning, you'll lead a computer through solving the problem. The difference is mostly in specificity: computer languages are simpler, are executed faster, and aren't as forgiving of mistakes.

First I reason about a problem. I try to phrase it in a simple way to myself. Break it into subproblems which can be solved easily. Develop a notation to talk about it, draw diagrams, walk through simple cases step by step, and look up how other people solved it. Sometimes this takes seconds, other times days.

Then I write it in code. I break it up into functions, each of which expresses a simple, individual idea. I decide on common names for the things I'm trying to discuss, and use them consistently. Then I assemble the functions together into one that solves the problem. Each function or logical group has “comments”, which explain why the solution works this way and fills in contextual gaps for humans. Code always has two readers–the computer, and the person who comes in weeks or years later to change or improve it. Your job is to express the solution clearly and efficiently to both.

Third, I test the solution. I think of example cases–if I'm testing addition, I know that 1 + 1 is 2, and -3 + 5 is 2. Good software carries with it a test suite full of these demonstrations, which verify every piece of the program.

Finally, I refine. Maybe the program wasn't formatted correctly, or I mis-spelled a word. Maybe there was a logical error. The compiler (thing that turns the language into a running program) and your tests work together to demonstrate that the solution is correct. Maybe it's correct, but it's too slow. I figure out where the problems are and redesign or optimize as necessary. This tends to be the hardest part.


## Bức tranh lớn hơn

Viết một phần mềm phức tạp, cũng chính là quá trình thay đổi liên tục. Bạn sẽ đi qua nhiều bản nháp của một bài tiểu luận, khám phá nhiều thứ mới mẻ, sắp xếp lại, rồi duyệt bởi chính bạn hoặc với những người khác. Trong công việc phát triển, bọn tôi gọi một bản nháp là một "version". Có những phần mềm chuyên dụng để kiểm soát những version này (Version Control Software), nó sẽ lưu tất cả versions và kết nối chúng lại thành một mạng khổng lồ. Nó cho phép chúng tôi hiểu về lịch sử thay đổi của một tài liệu, và quan trọng hơn, nó còn cho phép tích hợp thay đổi đến từ mỗi người (**làm việc chung**).

Khi nhiều người cùng làm phần mềm, chúng tôi cố gắng chia nhỏ nó ra. Như vậy mỗi người có thể làm trên một thành phần riêng rẽ và ko gây trở ngại tới người khác. Có rất nhiều cách tổ chức Mã Code, những cách này đều hướng đến việc chia nhỏ, phân loại sự phức tạp để giúp bạn có thể hiểu và thay đổi được những phần nhỏ một cách riêng lẻ.

Tưởng tượng việt viết một paper với một người bạn. Các bạn mỗi người nhận viết một section riêng, rồi sau đó kết hợp nó lại thành một tài liệu. Sau đó bạn có thể đọc phần của người còn lại và mở rộng nó, bạn có thể thay đổi từ ngữ, sắp xếp lại câu chữ. Môi lần bạn thay đổi thì bạn có thể lưu một "version" mới, và các bạn so sánh ghi chú vào buổi tối, bạn có thể coi mỗi thay đổi một cách độc lập, và quyết định cái nào sẽ phù hợp với toàn bộ tài liệu. Những thay đổi nhỏ thì càng dễ so sánh và tổng hợp hơn, nó cũng giúp bạn hiểu về lịch sử của tài liệu đó. Khi bạn tìm thấy một đoạn văn bị mất, bạn có thể đọc lại lịch sử để xem tại sao nó biết mất và biến mất ở giai đoạn nào.

## Những công cụ thông dụng

If you want to go for a career in tech I'd focus on building the most universally applicable skills first. It requires a bit of abstract, up-front investment, but they'll help you work faster in the long run and are skills you continually reinforce. Think of this part like an intro class in finding sources, structuring an essay, etc.

First: You'll need an operating system. Honestly, most of the tools you'll be using just aren't designed for Windows. It's possible to get along but it can be clunky. Linux is probably choice #1, and Mac OS a common second. Many windows-based devs I know run Ubuntu in a virtual machine.

http://www.psychocats.net/ubuntu/virtualbox

Second: you need an editor, something that lets you write text. Some folks start with Textmate, Sublime Text, or Notepad++, but the best programmers I know use Emacs or (my preference) Vim. They're both powerful, but will feel awkward while training muscle memory. You can always switch later, but folks tend to stick with their early choices. It's like driving stick vs auto. Some languages like Objective C or Java need a lot of contextual information–like foreign language dictionaries, proofreaders, etc, to write well. If you work in one of those languages, you'll probably adopt a specific kind of editor, called an IDE, designed to help you.

Third: version control. There are a lot of choices, but most people and projects I work with use Git and Github. You can pick up the basics in a half hour and it'll make your life super easy as you start working on a project.

## Ngôn ngữ lập trình

OK here's where I bring in personal opinions. Everyone's got em, ask a different person and you'll get different answers, often strongly felt. You'll start to develop these as you explore. Whatever you're using right now is The Best Language.

Javascript is a… necessary evil, and not the worst thing in the world. It's the only way to write frontend interactive code, so if you want to build interactive web pages you'll need to use it. It was thrown together quickly as a language, so its design suffers as a result. There are many special cases. Organizing code is difficult. The “things” in the language like numbers, strings, and lists can change type unexpectedly. Understand that when you write Javascript you can feel frustrated or confused and not know why; part of the reason is because the language itself is limited. It's a pidgin.

There's another class of frontend design, and that's for phones and tablets. The two big players are IOS (e.g. the iphone and ipad), which uses a language called Objective-C, and Android, which uses a language called Java. They're roughly equivalent in complexity and language power, like French and German. I'd say they're both middling in expressiveness. They're more… finicky than writing backend code. More special cases, a little harder to get started. That said, there's nothing like the power of making a magic thing happen in the palm of your hand, and if abstract problems aren't as interesting this can be a great niche.

On the backend, your choices are a lot wider. Lots of folks are using Ruby or Python. Like French and Spanish, they're both common, closely related, and roughly equal in performance and power. Because they're widely adopted you'll find libraries (chunks of code you can put together to solve specific problems) for almost everything.

For performance, big shops like to use Java, and to a lesser extent, C or C++. Java is reasonably fast but quite large, as a language, and slow to improve. I find it… muddy to write in. It's like not being able to use commas, and having to break every thought into a distinct simple sentence. C and its variants are extremely fast but can be more dangerous. I'd advise these as second languages.

I would avoid PHP and Perl. They're OK languages but suffer from… agglomerated cruft, and there's no particular strength to recommend them. PHP lacks design restraint and ended up a bit like English: nobody can agree on what words to use.

Lisp (remember the language you learned last time we talked?) and its variants are a bit like Latin. Very old–one of the first, actually. Radically simple. Incredibly expressive. Very few speakers, although that's changing with Clojure. Almost every other language can be viewed as a subset of Lisp. It… changes you, the way you think, in fundamental ways. Makes you a better programmer in other languages.

When you start programming, your thoughts will be small and concrete, just like in any new language. As you grow, you'll start to solve bigger problems, more abstract problems. Every language has a sort of.. abstraction ceiling, above which you can't express ideas directly. For instance, English will let you define new names for objects you haven't encountered before. German will let you generate compound verbs, but in practical terms English and German are roughly equivalent in descriptive power; they just approach the problem differently. Most computer languages are like that. Lisp… lets you invent new grammar on the fly.

That said, there aren't many folks hiring in Clojure or other Lisps, though they are out there and the jobs are cool. I recommend playing with it, if you have the time.

Most modern languages are very similar. Ruby, Python, Perl, PHP, Java, and C are all Germanic, insofar as they share close conceptual ancestors. There are whole other families of languages out there which you should be aware of, analogous to Japanese or Arabic, though not many people are using them. In particular, Haskell and OCaml are strongly typed functional languages which look quite different from any other–and have a higher abstraction ceiling. Erlang is a functional distributed language where code can live across many computers at once. If you choose to pursue these sorts of languages it can be extremely rewarding (and make you an excellent programmer), but you may have to study for longer before finding a job.

## Giả định công việc đầu tiên

You'll start learning a language, and gain experience with the fundamental tools. Over time you'll build a project that drives you to learn specific libraries for a task, like drawing pictures, storing data, or serving web pages. As you gain confidence you'll start writing code that exemplifies your style and skill. All your projects are published on Github. Nobody notices.

When you feel ready, start putting out feelers. Your portfolio has a few small projects–maybe demos, maybe libraries–which show your ability to write clear, documented, testable, code. You start sending your resume around, and link to your github account. Folks read the code, and see potential.

You land a job at a small startup, and fumble your way through a million things nobody thought to tell you. You feel useless for a bit, but start to catch on. In a month (heck, maybe your first day) your first code hits production, and something you built is on the screen for ten thousand users. The problems at your job spur you to learn new libraries, algorithms, and languages. You write some code to help talk to a natural language parsing service, and your boss says sure, throw it up on github.

From there it sort of cascades. As your open-source profile grows in quality and reach, more people will start to take notice of your code. Maybe you get a promotion internally, or move to another company. You'll have the latitude to branch out a fair bit at a startup, and learn from your peers.

## Ok, bắt đầu khởi động nào, Kyle

Option A: Towards frontend development.

You and I write a tiny web site together, tomorrow. Something super basic, like a notepad. We can get you started with Ruby as a language, Sinatra for a server framework, and HTML+CSS to show the page. Should only take a hundred lines or so, and you'll have a skeleton to start exploring on your own. You'll get an overview of the “full stack” from frontend to backend, and version control. OTOH, you'll be learning three distinct languages at once, which can get confusing. Testing frontends is extremely challenging, so we won't discuss that aspect much. On the other hand, you can see the results in the browser, which can feel great.

Option B: Towards backend development.

We work through some Project Euler problems together. They're bite-size math problems and each has a single answer, so there are clear goals and you get the satisfaction of solving each in turn. They start easy and get harder, and introduce you to powerful techniques along the way. We can use any language, but I'd recommend Clojure or Ruby. This path would introduce you to testing, algorithms, debugging… the process of problem solving in code. You only have to learn one language, which can give you a leg up on tackling A later. It'll push you to deeply understand a given language and advanced techniques.

Option C: Build something you care about.

Take any problem you think is interesting. Make it personal. Doesn't matter if anyone else cares, you just need something that'll drive you to think about and solve it. Maybe you want to… translate Latin texts automatically, make a chat client, plot your weight, index papers, make a videogame… whatever. I'll help you design a solution in any language.

And of course you can switch between these whenever you get bored. All of these paths will broaden over time and introduce you to the language and techniques you'll need for a job.

–Kyle


