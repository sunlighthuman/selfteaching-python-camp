## Day10
day10的作业是要求词频统计，要求引入一个外部的库**结巴**,听起来很傻，但确实一个厉害的断词的库。
结巴一共有三种模式：
>全模式、精确模式、搜索模式

作业要求的是精确模式。这是一个很神奇的库，有点类似于我们小学时候老师教的断句。
>我/来自 /云南省/曲靖

以前是我们用自己的小脑袋来识别断句，现在是教会程序断句，我们直接调取来用就行了。

想想我们现在所调试的函数，封装起来的话也算是勉强拿的出手给别人用用的库了吧。


## Day9
改写了好几天的函数，对函数有了一点点更加深入的认识.今天布置的作业是要在前几天作业的基础上加上collections.Counter most_common([n])这个函数，当看到这个函数中这一行介绍时有点难过
```
>>> Counter('abracadabra').most_common(3)  # doctest: +SKIP
[('a', 5), ('r', 2), ('b', 2)]
```
意味这我前几天写的函数是一个重复啰嗦的函数，而我只要调用已经封装好的函数，我写的那几行代码完全可以删掉了。于是我原本的函数：
```
import re
def stats_text_en(t_en): 
    if not isinstance(t_en,str):
        raise ValueError('输入的不是文本格式，请重新输入：')
    '''英文词频统计'''
    a = t_en.replace(',','').replace('.','').replace(':','').replace(';','').replace('"','').replace('!','').replace('?','').replace('、','').replace('，','').replace('。','').replace('“','').replace('”','').replace('：','').replace('；','').replace('\n','').replace('！','').replace('？','').replace('/','').replace('*',' ').replace('--',' ')
    a = a.lower()
    a = re.sub("[^A-Za-z]", " ", a)
    a = a.split() 
    b = {}
    for i in a:
        count =  a.count(i)
        r1 = {i:count} 
        b.update(r1)
    c = sorted(b.items(),key=lambda x:x[1],reverse=True) 
    print('英文单词统计频率如下： \n',c)
```
可以精简成如下函数：
```
import collections
import re

def stats_text_en(t_en,count): 
    '''该函数返回一个英文单词词频统计，样式为（word,count）'''
    if type(t_en) == str:
        text_en = re.sub("[^A-Za-z]", " ", t_en.strip())
        enlist = text_en.split() 
        return collections.Counter(enlist).most_common(count)
    else:
        raise ValueError("输入不为字符串")
```
还有就是几乎可以嗅到一件可怕的事，那就是我好几天就看到counter函数了，而我只要在官方文档里查查看就可以试着拿来用，而我没有，这就意味这我的“未经声明，不能引用”的内置程序启用了，得赶紧删除了。



=======
>>>>>>> upstream/master
## Day8
短跑过半了，坚持，坚持！

## Day7

又是在前一天的基础上完成任务，虽然看着很简单的，但依然折腾了一天，开始是在jupyterlab上测试，老是显示错误，后面在Terimal中测试又可行。我把anaconda,jupyterlab等全部升级了一遍后不显示错误了，但还是有地方不对，因为第二个调用函数，虽然执行了结果，但会返回连个None,None.不清楚，不明了。

## Day6
心得如下：

1.进行到这一部分的时候干了一件蠢事，因为一看到要做一个函数，心理比较慌，下意识的去看了下别人是怎么做的，意图参考，然后我渡过了最难过的2天。
>别人的鞋不合脚呀

想了一下午才想明白，其实day6的内容早在day5就完成了一大半，我只要把day5的内容改装一下封装进day6的函数就可以了呀，真是蠢到家了，然后在1个小时内就把两个函数写出来了。

2.别人的作业也不是不可看

>但要合理借鉴

我参考过两个同学的作业，一个同学写的简单，但两个函数只能单独统计。就是一个函数只能统计*纯英文*，另一个函数只能统计*纯中文*。

然后是1班同学的，那叫一个复杂，直接调用了collections（集合） 和 re（正则表达式）模块，看不懂，想抄都没有办法。

我的作业本来也是两个函数分开统计纯英文或者纯中文，但我实在想改进一下，让函数能够区分中英文，在统计英文的时候去掉中文，统计中文的时候去掉英文。然后就注意到了尖子生的正则表达式。
>虽然不懂，但不妨碍我拿来用。

试了一下调用正则表达式模块，果然可以用，心理高兴极了，吃饭都嫌麻烦，调试了半天。

3.我现在把这个正则表达式函数列出给大家看看，以防大家可以用到。
```
import re # 调用正则表达式模块
a = "simple is better than complex简单比复杂更好"
b = re.sub("[^A-Za-z]", " ", a) # re.sub(pattern, repl, string, count=0, flags=0)
c = re.sub("[A-Za-z]", "",a) # 注意A前面的^,对比下结果你应该明白这个符号是干嘛的
print(b)
print(c)
```
输出结果
```
simple is better than complex        
    简单比复杂更好
```
另外，大家感兴趣可以根据我的学号去看看我的作业，在大作业仓库的exercises文件夹中，应该相对简单一点。


## Day5

一天不敲代码，现在总觉得心里面空唠唠的。今天是清明节假期，敲代码上瘾。

这一次的收获：

1.慢下来总能对代码有所理解的，学习后面的内容总能对前面的内容有更进一步的认识和理解。

2.怕麻烦真的好费钱呀
>怕麻烦的人的钱都被不怕麻烦的人赚走了

3.假期要拿来好好学习，要好总结下《自学是门手艺》第一部分的内容。


## Day4

今天有点难过，任务是编一个乘法表，要求用for...in..等语句完成任务。我翻看了这一章介绍后，感觉无从下手，就像给你工具，材料，然后让你砌墙时，从来没砌过墙的你拿着工具盯着作业场地有点茫然。没有办法，还是先看看别人是怎么完成的吧。搜到几个教程，很花哨，有花式排列乘法表的，有加了制表函数，做成带框表格的。没有理那些YYJH,我还是找了个自己看得懂的慢慢琢磨。
>老司机才炫技，新手还是乖乖跟着开慢车吧。

#### 心得要点

1.for循环跟range()函数是个固定搭配，例如：
```
for i in range(10):
    print(i)
```
这个表达式会列出0-9这10个数字。

2.过程中我是先照者别人的写一遍，可以执行后，我又换个参数自己慢慢写一遍，看不懂的地方我就挪挪位置，换个方式，改变下参数看看会有什么变化，以便自己可以更理解这个写法。比如最开始的乘法表我把<print ()>这一行去掉了，也能运行，但结果是没有阶梯排序的乘法表。虽然还是不理解是什么原理，但我知道了这一行的重要性。同理我把去偶数乘法表最下面的<y += 1>,和<x += 1>去掉后,引发了程序的无限循环，看来这两行也挺重要，应该是终止循环的语句。

3.在第二个去除偶数的任务中，参照了别的编程营小伙伴的作业，但觉得他们那个编写方法看不明白，我就想起了不是有break语句吗，怎么都没人用，我就自己尝试了下，写入：
```
if x % 2 == 0: # 如果x除以2余数为零，说明是偶数，那么就终止
    break
```
敲入结果一看，果然把左边的偶数干掉了，不禁有点小开心，貌似是比小伙伴们找到了个更好的解决方案。


## Day3

今天的课程是要编写一个计算器，如果说前两天是带你认识工具的话，今天直接就要你用工具做出一个产品来了。画风不对呀，虽然有说明书，但怎么感觉中间少了n个要学的东西，懵了。

还好我们有“老师”--“谷歌，必应”，大作业仓库，厚着脸皮先看看尖子生是怎么写的，再把别人的计算器“拆了”，自己组装一下。

看了下别人的程序实现，有超级复杂的，调用了tkinter模块，直接输出了一个计算机可视化界面，跟win上的类似；也有超级简单的，只调用了int(),input(),print()函数利用if语句就实现了；也有隔壁的尖子生，直接定义函数实现的。

我照着最简单的方法敲了个最简单的计算器，不仅有“加、减、乘、除法”，我自己加上了“幂、余”都能实现，然后我发现原代码不支持小数计算，翻看了一下函数那章，换了个float()浮点数函数就可以实现小数运算了，代码如下：
```
# float()支持小数运算
# 如果用int()函数的话就只支持输入整数
# input()接收键盘输入

a=float(input('请输入数值1'))  
b=input('请输入运算符号')
c=float(input('请输入数值2'))
if b=="+":
    print(a+c)
elif b=="-":
    print(a-c)
elif b=="*":
    print(a*c)
elif b=="/":
    print(a/c)
elif b=="**":
    print(a**c)
elif b=="%":
    print(a%c)
```

然后我试了试第二种方法，也是可以用的：
```
choice = float(input('请选择运算： \n1.加\n2.减\n3.乘\n4.除\n5.幂\n6.余\n请选择你的算法： '))
num1 = float(input('请输入第一个数： '))
num2 = float(input('请输入第二个数： '))
if choice == 1:
    print('{} + {} = {}'.format(num1, num2 ,num1+num2))
elif choice == 2:
    print('{} - {} = {}'.format(num1, num2 ,num1-num2))
elif choice == 3:
    print('{} *{} = {}'.format(num1, num2 ,num1*num2))
elif choice == 4:
    print('{} / {} = {}'.format(num1, num2 ,num1/num2))
elif choice == 5:
    print('{} ** {} = {}'.format(num1, num2 ,num1**num2))
elif choice == 6:
    print('{} % {} = {}'.format(num1, num2 ,num1%num2))
```
以用带练，多学多用！

## DAY2
今天在运行hello world程序的时候踩了个莫名其妙的坑，那就是输入print函数括号里面的点符号踩的坑。我开始输入的是esc下面那个`，因为为看着别人好像也是输入的这个，然后程序一直报错，我快疯了，后面换了"才没有报错，最后我才发现是这个'（“不用shift的')。

#### 建立hello_world.py文件的方法有三种：

1.在vscode中可以直接通过点击建立。

2.通过终端建立，在cd 文件夹后，输入
```
touch hello_world.py
````
这个方法在windows中会报告错误，没找到解决方案，我是在电脑上用virtualbox安装了ubuntu系统然后在Ubuntu系统中的终端上实现的。

3.直接在jupyterlab中建立一个hello_world.ipyb文件。

#### 执行hello_world.py的方法有三种：

1.打开终端，cd打开hello_world.py程序所在的文件夹,执行
```
python hello_world.py
```
可以看到输出结果

2.在vscode中右键单击hello_world.py再点击在终端中运行也可以看到输出结果

3.在jupyterlab中直接shift+enter，也可以直接看到输出结果。

## DAY1
今天进行了自学营的第一次训练，本来以为自己已经早就熟练掌握了github的创建仓库，提交更改之类的，但是今天发现自己仍然只是知道一部分。参加自学营前参加了刘娟娟的"you can you up,no bb"以为自己闯过了第一关，守关人跟我说你并没通过的时候，我理直气壮的跟他说，我完成了呀。守关人并没有说什么，让我去了第二关，今天才知道我真的是没有通过，人家一看截图，没有分支，没有commit，真是懒得理我。学习真的是切记骄傲啊。





