# Project01
### Multiple pressure switches with RGB LED control using state machine and color transitions
"Ogre Pastry Chef" revolves around an ogre who loves to bake delicious desserts. The user needs to press buttons representing human organs to select ingredients for making cakes.

### State Diagram




### Function
There are three pressure switches:
Each pressure switch controls a different LED strip display effect.
When the first pressure switch is pressed, the RGB LED strip displays white
When the second pressure switch is pressed together with the first, the RGB strip display gradually changes to pink
When all three pressure switches are pressed at the same time, the RGB strip gradually changes to dark red.

Code snipped for state setting

```Python
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
```

Code snipped for state changing

```Python
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
```
I used a double layer of paper to avoid exposing the copper tape traces.
I drew the circuit structure on the bottom layer of paper to facilitate later operation.
(Picture)
I soldered the wires through the small holes in the bottom layer of paper to the copper tape to make it strong and ensure that all the hardware connection parts were covered in the acrylic frame.
(Picture)
