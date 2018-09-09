## 1. 基本概念
	1. 数
		a. 整数：2
		b. 长整数：
		c. 浮点数：3.23
		d. 复数：

	2. 字符串
		a. 单引号
		b. 双引号
		c. 三引号（'''或""")，中间可随意输入单引号和双引号
		d. 转义符
		e. 自然字符串，在字符串前添加r或R，用于正则表达式，无需转义太多的反斜杠
		f. Unicode字符串，字符串前加上前缀u或U
	3. 变量
		a. 字符或者_开头，后可跟数字，字符，下划线
		b. 大小写敏感
    

## 2. 表达式
### 2.1. 运算符
		**	幂	返回x的y次幂	3 ** 4得到81（即3 * 3 * 3 * 3
		//	取整除	返回商的整数部分	4 // 3.0得到1.0
		%	取模	返回除法的余数	8%3得到2。-25.5%2.25得到1.5
		<<	左移	把一个数的比特向左移一定数目	2 << 2得到8。——2按比特表示为10
		>> 	右移	把一个数的比特向右移一定数目	11 >> 1得到5。——11按比特表示为1011，向右移动1比特后得到101，即十进制的5。
		|	按位或	数的按位或	5 | 3得到7。
		&	按位与	数的按位与	5 & 3得到1。	
		^	按位异或	数的按位异或	5 ^ 3得到6
		~	按位翻转	x的按位翻转是-(x+1)	~5得到-6。
		<	小于	返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。	5 < 3返回0（即False）而3 < 5返回1（即True）。比较可以被任意连接：3 < 5 <7返回True。
		>	大于	返回x是否大于y	5 > 3返回True。如果两个操作数都是数字，它们首先被转换为一个共同的类型。否则，它总是返回False。
		<=	小于等于	返回x是否小于等于y	x = 3; y = 6; x <= y返回True。
		>=	大于等于	返回x是否大于等于y	x = 4; y = 3; x >= y返回True。
		==	等于	比较对象是否相等	x = 2; y = 2; x == y返回True。x = 'str'; y = 'stR'; x == y返回False。x = 'str'; y = 'str'; x == y返回True。
		!=	不等于	比较两个对象是否不相等	x = 2; y = 3; x != y返回True。
		not	布尔“非”	如果x为True，返回False。如果x为False，它返回True。	x = True; not y返回False。
		and	布尔“与”	如果x为False，x and y返回False，否则它返回y的计算值。	x = False; y = True; x and y，由于x是False，返回False。在这里，Python不会计算y，因为它知道这个表达式的值肯定是False（因为x是False）。这个现象称为短路计算。
		or	布尔“或”	如果x是True，它返回True，否则它返回y的计算值。	x = True; y = False; x or y返回True。短路计算在这里也适用。

### 2.2. 控制流
#### a. if&while
		number=15153
		running=1
		while running:
		  guess = int(raw_input('enter an interger:'))
		
		  if guess == number:
		    print "you win"
		    print "(but you don't have gift)"
		    running=False
		  elif guess < number:
		    print "litter than"
		  else:
		    print "larger than"
		print "all done"
		
#### b. for
```
l = [i for i in range(1,5)] 
for i in l:
    print(i)
```

		
#### c. while True:
		  s = raw_input('Enter something: ')
		  if s == 'quit':
		    break
		  if len(s) < 3:
		    print 'value is too small'
		    continue
		  print 'Length is',len(s)
		print 'done'
		
### 2.3. 函数
		a. DocStrings，按以下规则但不强制，调用方式为：function.__doc__
			i. 首行大写
			ii. 句号结尾
			iii. 第二行空行，第三行详细描述
		b. dir()
		
## 3. 数据结构
	1. list
		mylist=['a','b','c']
		len(mylist)
		mylist.append('d')
		del mylist[2]
		mylist.sort()

	2. 元组
		zoo=('a','b','c')
		new_zoo=('d','e',zoo)
		print zoo,len(zoo)
		print new_zoo,len(new_zoo)
		print new_zoo[2]
		print new_zoo[2][1]
		age = 22
		name = 'Swaroop'
		print '%s is %d years old' % (name, age)
		print 'Why is %s playing with that python?' % name

	3. 字典（键值对）
		ab={1:'a',2:'b',3:'c'}
		print ab
		print ab[1]
		ab[0]='agagd'
		print ab
		print ab[0]
		del ab[2]
		print ab,len(ab)
		for i,j in ab.items():
		  print i,j
		if 2 in ab:
		  print ab[2]

	4. 序列
		['a', 'b', 'c']
		seq[0] a
		seq[1] b
		seq[2] c
		seq[-1] c
		seq[-2] b
		seq[0:2] ['a', 'b']
		seq[1:] ['b', 'c']
		seq[0:-1] ['a', 'b']
		seq[:] ['a', 'b', 'c']
		以下方式可灵活用于字符串截取：
		name = 'swaroop'
		print 'characters 1 to 3 is', name[1:3]
		print 'characters 2 to end is', name[2:]
		print 'characters 1 to -1 is', name[1:-1]
		print 'characters start to end is', name[:]
		列表综合
		a=[1,2,3]
		b=[2*i for i in a if i > 1]
		print b # [4,6]

	5. 字符串方法
		name.startwith('S')
		'a' in name
		name.find('a') #-1 找不到
		delimiter.join(list)
		print 'value is',a #带空格
		print 'value is'+a #不带空格
		print 'info:', #不换行
		name.replace('a','b')

## 4. 类库
	1. time
		time.strftime('%Y%m%d%H%M%S')
		os
		os.system('pwd')
		os.path.exists('/root')
		os.mkdir('/root')
		os.sep

	2. file
		f=file('s.txt','w') # w,r,a(追加)
		f.write('xxx')
		f.close
		while True:
		  line=f.readline()
		  if len(line)==0
		    break

	3. cPickle
		import cPickle as p
		shoplist=['a','b','c']
		f=file('s.txt',w')
		p.dump(shoplist,f)
		storelist=p.load(f)

	4. except
		try:
		  ...
		except EOFError:
		  ...
		except:
		  ...
		else:
		  ...

	5. finally
		try:
		  ...
		finally:
		  ...

  6. cat
[root@localhost mypython]# cat cat.py
#!/usr/bin/python

import sys

def readfile(filename):
  f=file(filename)
  while True:
    line=f.readline()
    if len(line) == 0:
      break 
    print line,
  f.close()

if len(sys.argv) < 2:
  print 'no action'
  sys.exit()

# sys.argv[1].startwith('--'):
if sys.argv[1][0:2] == '--':
  if sys.argv[1][2:] == 'version':
    print 'cat version - 1.2'
  elif sys.argv[1][2:] == 'help':
    print 'Usage: xxx'
  else:
    print 'unknow option'
else:
  for i in sys.argv[1:]:
    print 'reading file %s' % i
    print '----------------------'
    readfile(i)
    print

