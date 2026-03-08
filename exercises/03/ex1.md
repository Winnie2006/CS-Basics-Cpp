```h0```  大数加法
输入的两个数大小为$1<=a,b<=10^{100}$
输出两数之和

【分析】
显然，所有整型的数据类型都不足以储存$10^{100}$量级的数：

| ```int```                | 4B(32b) | -$2^{31}$ ~ $2^{31}-1$ |
| ------------------------ | ------- | ---------------------- |
| ```long long```          | 8B(64b) | -$2^{63}$ ~ $2^{63}-1$ |
| ```unsigned int```       | 4B      | 0 ~ $2^{32}-1$         |
| ```unsigned long long``` | 8B      | 0 ~ $2^{32}-1$         |
所以，我们可以将输入的数存为字符形式，然后进行“手动”加法
Note：
- 数组长度设置成$10^{100}$会“内存溢出”!
->**常用方法：用```std::string``` 实现“动态内存分配”！**
与此同时，**C++的```string```库**简化了内存管理、长度计算、拼接操作！
->其他方法：```std::vector<int>```!


【解答】

steps:
1. input and store each character in the char array until the end (newline/ space) and add '\0'.
2. get the size of both "numbers"
3. add with a carry (like 270) 先补长再相加？还是？
4. output the final result stored in a new character array

【痛点总结】
- 大数不会处理，int不行，char array也不行，
- string不会用：用库函数基本操作不会
- 算法实现，能意识到问题，但没有成熟的“技巧”/“实现惯例”解决，脑子里不清晰不能画流程图，时而纠结于细节，时而纠结于整体实现：
	- 翻转问题（在想for循环）
	- 补位问题（if/三元运算符）
	- 进位问题（“在什么地方”加carry?)



