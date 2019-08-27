# python 技巧  

1. python利用*号对可迭代的对象进行解压，并赋值给多个对象。
##	
	record = ['lakers','76ers','warriors']	  
	*teams,team = record  
	print(*teams)
	out：lakers 76ers
*号表达式也可以应用于列表的开始部分以及字符串的分割，若想解压一些元素而不使用，则使用一个普通的'_'或'ign'即可。在迭代元素为可变长元组的序列时很有用。
##
	records = [
        ('no1','76ers'),
        ('no2','warriors'),
        ('no1','bull')]

	def bar(s):
    	print('no1',s)

	for tag,*args in records:
    	if tag == 'no1':
        	bar(*args)
	out:no1 76ers
	    no1 bull
其中records为一个带有标签的元组序列.

2. 如何保留最后N个元素

##	
	from collections import deque

	def search(lines,pattern,history = 5):
    	previous = deque(maxlen=history)
   	 	for line in lines:
        	if pattern in line:
            yield line,previous
        previous.append(line)
在多行上做简单的文本匹配，并返回匹配所在行的最后N行。使用deque（maxlen=N)构造函数会新建一个固定大小的队列。当新的元素加入并且这个队列已满，最老的元素会自动被移除掉。


