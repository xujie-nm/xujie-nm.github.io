今天学习python的一些感悟


#timer
"""
关于python编程的思考：
	python编程现在我觉的它的最大的一个特点，就是把
	事件分为好多个不相干的子事件
	例如这个程序：
		一个简单的屏幕保护程序：
			把想要显示的message设为一个事件
			把定时的改变位置设置一个事件
			如果可以的话还可以把时间间隔设置为一个事件
			最后综合起来画图设置为一个事件
			适当的分解程序
			
			重点是互不相干
			
			问题：为什么改变了变量position，而不用声明
			global？
			答：因为它只是依次的改变了position的元素，而
			没有改变position本身
"""

import simplegui
import random

# global state

message = "Python is Fun!"
position = [50, 50]
width = 500
height = 500
interval = 2000

#Handler for text box
def update(text):
    global message
    message = text
    
#Handler for timer
def tick():
    x = random.randrange(0, width)
    y = random.randrange(0, height)
    position[0] = x
    position[1] = y
    
#Handler for draw on canvas
def draw(canvas):
    canvas.draw_text(message, position, 36, "Yellow")
    
#Create a frame
frame = simplegui.create_frame("Home", width, height)

#Register event handler
text = frame.add_input("Message", update, 150)
frame.set_draw_handler(draw)
timer = simplegui.create_timer(interval, tick)


frame.start()
timer.start()
