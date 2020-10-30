며칠간 별 소득이 없자, 남들도 4시간 만에 끝낸다는 마법의 어셈블리를 집어들었다.

그런데 calling convention부터 시작해서 벌써부터 난관이다.

@jwon(github:jwon42)님의 코드와 디스코드에서 @chlee님이 추천해준 tutorialspoint를 참조하고있다.
(https://www.tutorialspoint.com/assembly_programming/index.htm)
그리고 한글로 번역된 PC Assembly PDF.. (https://pacman128.github.io/pcasm/)
과정이 NASM으로 진행되기 때문에 참조한 사이트 (https://opentutorials.org/module/1596/9755)
머리가 지끈지끈하다.

아래와 같이 아직 미완성 상태인데, 지금까지 알아본 것은
1. ;(쉼표)는 주석
2. section 부분은 segment라고도 써도 된다는데, 혼용해도 써도 되려나 싶은 부분
3. 코드 세그먼트(.text)부에서 프로그램 실행이 시작되는 위치를 커널에 알려주는 global _(func. name)을 해야한다는 점
4. global은 어셈블리에서 함수(?)가 선언되면 기본적으로 지역함수인데, 이를 외부에서 호출하기 위해서는 global로 해야한다고 함
5. .bss는 초기화하지 못한 변수를 최적화하기위한 영역 (https://studyforus.com/Hygon/311551) <- 세그먼트 별로 너무 잘 정리되어 있는 것...
6. jmp는 강제로 분기 명령을 하는 것. goto 명령과 같다는데 아직 goto를 안써봐서 실감이 되지 않는다는 것.

어쨌든 좀 빠르게 학습해야할 것 같은 예감이 들었다. 한 1주일 걸릴 것 같은데...

```
;prototype
;size_t		strlen(const char *s);

section	.data			;data segment

section .bss			;bss(block started by symbol) segment

section	.text			;code segment
	global _ft_strlen	;must be declare for linker (ld), globlized label

_ft_strlen:				;tells linker entry point(C calling convention)
	mov	rax, 0			;initialize rax value, rax will be return value
	jmp _count			;(forced)branch instruction

```
