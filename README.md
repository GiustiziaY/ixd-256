# ixd-256
```Python
import os, sys, io
import M5
from M5 import *
from hardware import *
import time

print('Multiple pressure switches with RGB LED control using state machine and color transitions')

# 初始化 M5 板
M5.begin()

# 配置 RGB 灯带，假设灯带连接到 G2 引脚，包含 10 个灯
rgb_strip = RGB(io=2, n=10, type="SK6812")

# 配置三个压力开关引脚为输入，并带上拉电阻
switch1 = Pin(8, mode=Pin.IN, pull=Pin.PULL_UP)  # 压力开关1 (pin 8)
switch2 = Pin(7, mode=Pin.IN, pull=Pin.PULL_UP)  # 压力开关2 (pin 7)
switch3 = Pin(6, mode=Pin.IN, pull=Pin.PULL_UP)  # 压力开关3 (pin 6)

# 设置RGB颜色函数
def get_rgb_color(r, g, b):
    return (r << 16) | (g << 8) | b

# 颜色设置函数
def set_rgb_color(r, g, b):
    rgb_color = get_rgb_color(r, g, b)
    rgb_strip.fill_color(rgb_color)

# 渐变函数，用于在一段时间内平滑过渡颜色
def fade_rgb(start_r, start_g, start_b, end_r, end_g, end_b, steps=100, delay=10):
    for i in range(steps):
        r = start_r + (end_r - start_r) * i // steps
        g = start_g + (end_g - start_g) * i // steps
        b = start_b + (end_b - start_b) * i // steps
        rgb_strip.fill_color(get_rgb_color(r, g, b))
        time.sleep_ms(delay)

# 定义状态变量
program_state = 'IDLE'  # 初始状态为IDLE（空闲）

# 定义状态机中的各个状态
def update_state():
    global program_state

    if switch1.value() == 0 and switch2.value() == 1 and switch3.value() == 1:
        program_state = 'RGB_WHITE'  # 当按下 Pin 8 时，灯带变为白色
    elif switch1.value() == 0 and switch2.value() == 0 and switch3.value() == 1:
        program_state = 'RGB_PINK'  # 当按下 Pin 7 和 Pin 8 时，灯带变为粉色
    elif switch1.value() == 0 and switch2.value() == 0 and switch3.value() == 0:
        program_state = 'RGB_RED'  # 当按下 Pin 6, 7 和 8 时，灯带变为红色
    else:
        program_state = 'IDLE'  # 默认状态，什么都不做

# 状态执行逻辑，添加颜色渐变
def execute_state():
    if program_state == 'RGB_WHITE':
        fade_rgb(0, 0, 0, 255, 255, 255)  # 从黑色渐变到白色
    elif program_state == 'RGB_PINK':
        fade_rgb(255, 255, 255, 255, 105, 180)  # 从白色渐变到粉色 (RGB = 255, 105, 180)
    elif program_state == 'RGB_RED':
        fade_rgb(255, 105, 180, 255, 0, 0)  # 从粉色渐变到红色
    elif program_state == 'IDLE':
        set_rgb_color(0, 0, 0)  # 立即关闭灯带，不进行渐变

# 主循环
while True:
    M5.update()  # 更新M5板
    
    # 更新状态
    update_state()
    
    # 根据状态执行动作
    execute_state()
    
    # 延时，防止高CPU使用率
    time.sleep_ms(100)

```
