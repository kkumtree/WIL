@sucho(github:sungyongcho)와 함께 minishell을 처음부터 파고있다.  
기본 쉘로부터 환경변수를 받아와서 ':'를 기반으로 파싱하고 libft(library42)에서 권장하는  
key, value로 구성된 t_env를 콘텐츠로 꽂아 넣었다.  

```C
typedef struct  s_list
{
  void    *content;
  t_list  *next;  
}               t_list
```

단방향 맵로 만들고 뒤에 추가하는 함수까지는 기존에 이미 구현을 했지만,  
특정 키와 일치하면, 중간의 노드(content)를 삭제하고 이어붙일 방법을 궁리하고 있었다.  
(이러한 key-value 자료구조를 맵이라고 한다는 걸 지금 알았다)  

기본적으로 참조한 블로그는 여기 (https://sewo.tistory.com/18)

<img width="715" alt="list" src="https://user-images.githubusercontent.com/52643858/97719601-9b0ee680-1b0a-11eb-9d72-28ecef050146.png">

그림은 매우 간결하지만, 우리는 인자로 연결리스트 헤드와 키만 매개변수로 받아서 처리를 할 것이기 때문에  
머리를 약간 써야 했다.  

1. 단방향 리스트이기 때문에 앞의 노드를 미리 저장을 해줘야함
2. 메모리 해제를 챙겨줘야한다.

당연한 이야기지만, 앞의 노드를 저장하기 위해서 forward란 리스트 포인터를 선언하였다.  
맨 처음은 NULL로 지정하고, temp에 헤드를 옮겨담았다. (단방향 리스트의 헤드값을 잃어버리면, 효율적인 대책이 없기 때문에 이렇게 보완을 하였다)  
그 다음에 while문에서 빙글빙글 돌리면서 문자열이 일치하는지 검증하고 다음 리스트로 넘기는 것을 구현하였다.  
도중에 알게된 것은  
우리의 t_list의 content가 void *였기 때문에  
- key에 접근하기 위해서는 t_env라는 구조체라는 것을 명시해야한다는 것과  
- strncmp를 사용하여 완전일치를 검증하려면 문자열의 null값 위치도 검증해야하기 때문에 strlen + 1을 해야한다는 것이었다.  

그리고 segfault를 방지하기 위해서, 마지막 linked list가 끝나면 탈출하게 만드는 것은 'temp = temp->next'부분을 통해 해결하였다.  

```C
void	env_unset_one(t_list *env_head, char *del_key)
{
	t_list *temp;
	t_list *forward;

	temp = env_head;
	forward = NULL;
	while (temp)
	{
		if (ft_strncmp((((t_env *)(temp->content))->key), del_key, \
			(ft_strlen(del_key) + 1)) == 0 )
			{
				forward->next = temp->next;
				free(temp->content);
				return ;
			}
		forward = temp;
		temp = temp->next;
	}

}
```
