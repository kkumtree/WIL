오늘은 @sujung님과 @yohlee(github: l-yohai)님으로부터 도움을 받았다.  
일단 C calling convention에 대해서 이야기를 나누었다.  

code segment에서 전역변수화에 대해서 문의를 드렸는데,  
global _(labelname)을 쓸 때, 여기에 대해서 처음에는 굳이 언더스코어를 쓰지않아도 되지 않느냐라고 이야기를 나눴는데,  
실제로는 언더스코어를 빼는 순간, 정상적으로 작동하지 않았다. 컨벤션은 아래 글을 봐도 무엇을 말하고 싶은건지 아직 이해하지 못했다.  
(https://recoverlee.tistory.com/25)  

그리고 rax를 쓰게되는 이유를 들었는데, 어떤 크기의 자료가 들어올지 예상이 안되서 rax를 썼다고 말씀하셨다.  

그리고 클러스터 떠나기 전에 다른 주제로 이야기를 하였는데,  
@yechoi님이 쓰신 블로그글에 (https://yechoi.tistory.com/17) extern ___error 처리에 대한 내용이 있었다.  
이것은 strlen처럼 단순히 카운팅을 하는 func. 말고 write나 read처럼 system call을 쓸 경우 반드시 있어야 한다는 것이 요지였다.  

이 외에도 스택의 push, pop에 대해 이해가 어렵다고 하니, 이는 '프롤로그, 에필로그'를 찾아보라고 말씀을 주셨다.  
(https://m.blog.naver.com/s2kiess/30181227661)  
(https://shotgh.tistory.com/33)  

