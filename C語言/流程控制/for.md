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
