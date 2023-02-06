# for 述句
- for (初始式; 條件式; 迴圈式) {程式片段}
- 執行「初始式」。
- 當「條件式」 成立時， 執行 「程式片段」。 否則就結束迴圈。
- 執行「迴圈式」 後在回到上一步。
```
for(初始式; 條件式; 迴圈式){       
  程式片段                       
}                                
  // 相當於
  
初始式;
while (條件式) {
  程式片段
  迴圈式;
}
```
```
int count = 1;
while(count <= 10) {
  printf("%\n", count);
  count = count + 1;
}
 // 相當於
 int count;
 for(count = 1; count <= 10; count++){
  printf("%d\n", count);
 }
```
## 繪製三角形
```
#include <stdio.h>
#include <stdlib.h>
int main(){
	int N,x,y;
	while(scanf("%d",&N)==1){
		for(x=1; x<=N; x++){
			for(y=1; y<=x; y++){
				printf("*");
			}
			printf("\n");
		}
	}
	system("pause");
	return 0;
}
```
## [座標法繪製空心三角形](https://www.youtube.com/watch?v=8WJik0Dqdoc&list=PLY_qIufNHc293YnIjVeEwNDuqGo8y2Emx&index=94&ab_channel=FeisStudio)
- (1,1)(1,2)(1,3)(1,4)(1,5)(1,6)(1,7)(1,8)(1,9)
- (2,1)(2,2)(2,3)(2,4)(2,5)(2,6)(2,7)(2,8)(2,9)
- (3,1)(3,2)(3,3)(3,4)(3,5)(3,6)(3,7)(3,8)(3,9)
- (4,1)(4,2)(4,3)(4,4)(4,5)(4,6)(4,7)(4,8)(4,9)
- (5,1)(5,2)(5,3)(5,4)(5,5)(5,6)(5,7)(5,8)(5,9)
- (6,1)(6,2)(6,3)(6,4)(6,5)(6,6)(6,7)(6,8)(6,9)
- (7,1)(7,2)(7,3)(7,4)(7,5)(7,6)(7,7)(7,8)(7,9)
- (8,1)(8,2)(8,3)(8,4)(8,5)(8,6)(8,7)(8,8)(8,9)
- (9,1)(9,2)(9,3)(9,4)(9,5)(9,6)(9,7)(9,8)(9,9)

```
#include <stdio.h>
#include <stdlib.h>
int main(){
	int x, y, N;
	while(scanf("%d",&N)==1){               
		for(x=1;x<=N;x++){						 
			for(y=1;y<=N;y++){					 
				if(y==1 || x==N || x==y){		 
					printf("*");				 
				}else{							 
					printf(" ");				 
				}								 
			}									
			printf("\n");
		}
	}
	system("pause");
	return 0;
}
```
### 右三角
```
#include <stdio.h>
#include <stdlib.h>
int main(){
	int x, y, N;
	while(scanf("%d",&N)==1){               
		for(x=1;x<=N;x++){						 
			for(y=1;y<=N;y++){					 
				if(x+y >= N+1){		 
					printf("*");				 
				}else{							 
					printf(" ");				 
				}								 
			}									
			printf("\n");
		}
	}
	system("pause");
	return 0;
}
```
## 找簡易方程式解
#### 方法一
- 用座標法找要找900次(30*30)
```
#include <stdio.h>
int main(){
int x,y;
	for(x=1;x<=30;x++){
		for(y=1;y<=30;y++){
			if(x+y==30 && x*y==221){
				printf("%d, %d\n",x,y);
			}
		}
	}
	return 0;
}
```
#### 方法二 (x小Y大) *效率比方法一高*
- xy相加必然是30，分兩區塊
- x是1到15。y是15到30。
```
#include <stdio.h>
int main(){
int x,y;
	for(x=1;x<=30/2;x++){
		for(y=30/2;y<=30;y++){
			if(x+y==30 && x*y==221){
				printf("%d, %d\n",x,y);
			}
		}
	}
	return 0;
}
```
#### 方法三 (x小Y大)
- 一層迴圈
- 先知道x，那麼Y自然就知道
```
#include <stdio.h>
int main(){
int x;
	for(x=1;x<=30/2;x++){
		int y=30-x;
		if(x*y==221){
			printf("%d, %d,x,y");
		}
	}
	return 0;
}
```
