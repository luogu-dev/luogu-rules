当一个题目可以接受多种正确答案,即有多组解的时候,题目就必须被Special Judge．

Special Judge程序使用输入数据和一些其他信息来判答你程序的输出，并将判答结果返回．

洛谷的SPJ采用了跟Codeforces一样的SPJ标准，即Testlib库。

下载地址：


https://github.com/MikeMirzayanov/testlib/archive/0.9.12.zip

\_\_Checker的编译参数为：g++ -fno-asm -std=c++14 -O2 ，即已经开启C++14以及O2优化。\_\_

## 使用方法

只能使用c++。不过写spj就跟写别的题目一样，只是输入输出有所不同。首先新建文件checker.cpp。然后将这个压缩包的里的所有内容解压到你的checker.cpp相同的文件夹。


这里给出一个例子，当标准输出和选手输出的差小于0.01，那么可以AC，否则WA。

```cpp
#include "testlib.h"

int main(int argc, char* argv[]) {
    registerTestlibCmd(argc, argv);
    double pans = ouf.readDouble();
    double jans = ans.readDouble();

    if (fabs(pans - jans)<0.01)
        quitf(_ok, "The answer is correct.");
    else
        quitf(_wa, "The answer is wrong: expected = %f, found = %f", jans, pans);
}

```
在程序中，有3个重要的结构体：inf指数据输入文件（本例没有），ouf指选手输出文件，ans指标准答案。

然后，可以从这3表结构体读入数据，不需要用到标准输入输出。如果读到的数据和下面的期望不一致，则spj返回fail结果。


这边继续给出一个多行（不定行数）的spj判断：

```cpp
#include "testlib.h"

int main(int argc, char* argv[]) {
    registerTestlibCmd(argc, argv);

    while(!ans.eof()){
        double pans = ouf.readDouble();
        double jans = ans.readDouble();
        ans.readEoln();

        if (fabs(pans - jans)>0.01)
            quitf(_wa, "The answer is wrong: expected = %f, found = %f", jans, pans);

    }
    quitf(_ok, "The answer is correct.");
    return 0;

}
```

以下读入命令可以使用：

`void registerTestlibCmd(argc, argv)`

初始化checker，必须在最前面调用一次。

`char readChar()`

读入一个char，指针后移一位。

`char readChar(char c)`

和上面一样，但是只能读到一个字母c

`char readSpace()`    

同 readChar(' ').

`string readToken()`

读入一个字符串，但是遇到空格、换行、eof为止、

`long long readLong()`

读入一个longlong/int64

`long long readLong(long long L, long long R)`

同上，但是限定范围（包括L，R）

`int readInt()`        

读入一个int

`int readInt(int L, int R)`, 

同上，但是限定范围（包括L，R）`

`double readReal()`

读入一个实数

`double readReal(double L, double R)`, 

同上，但是限定范围（包括L，R）

`double readStrictReal(double L, double R, int minPrecision, int maxPrecision)`,

读入一个限定范围精度位数的实数。

`string readString()`, 

`string readLine()`    

碰撞一行string，到换行或者eof为止

`void readEoln()`    

读入一个换行符

`void readEof()`    

读入一个eof



`int eof()`

读完数据后，就可以开始spj了。选手程序能用的功能，spj一样能用。在洛谷中，spj照样受到时间空间限制。而且不能标准输入输出。

最后就是输出啦。输出跟printf有点像。

`quitf(\_ok, "The answer is correct. answer is %d", ans); `

给出AC

`quitf(\_wa, "The answer is wrong: expected = %f, found = %f", jans, pans); `

给出WA

`quitp(0.5,"Partially Correct get %d percent", 50);`

给出PC(Partially Correct)，并且可以获得该点50%的分数


## 测试

使用编译器将该文件编译。在命令行中输入:

```cpp
./checker in.txt out.txt ans.txt(Linux)
checker.exe in.txt out.txt ans.txt(Windows)

```
其中in.txt out.txt ans.txt分别是放在同一目录下的输入文件、选手输出、标准答案。

程序将返回结果。


## 上传与配置

直接将checker.cpp（必须这个名字）塞入测试数据的压缩包内然后上传就行了。

**重要：必须加上“Special Judge”标签**

**重要：必须加上“Special Judge”标签**

**重要：必须加上“Special Judge”标签**

很重要所以说三遍


然后，就没有然后了。


## Codeforces 赛制

由于 Hack 机制的存在，CF 赛制中 SPJ 是必须的。即使你有一个标程并且在 Hack 的时候直接比较这个标程的输出和用户程序的输出就可以判断 Hack 的有效与否，你也需要把这个标程改成 SPJ 的形式。也就是说，CF 赛制的题目数据包中必须有 checker.cpp 一个程序。


同时，还需要 validator.cpp 一个程序，用来验证提交的 Hack 数据的合法性，书写方式和规范同如上的 SPJ 说明，具体请参考 Testlib 的文档。