# FlashRL - Flash Platform for Reinforcement Learning
**Note that FlashRL is under heavy development. Breaking changes may occur**
**Note: This version of FlashRL has been forked to experiment with non-Keras ML frameworks**

Flash Reinforcement Learning (or FlashRL) is a framework for developing RL algorithms for flash games. It features several thousand game environments, some of which are ready to use without any modification.

If you use this work in your research, please cite the following paper :)
```
@article{NIK,
	author = {Per-Arne Andersen and Morten Goodwin and Ole-Christoffer Granmo},
	title = { FlashRL: A Reinforcement Learning Platform for Flash Games},
	journal = {Norsk Informatikkonferanse},
	year = {2017},
	keywords = {},
	issn = {1892-0721},	url = {https://ojs.bibsys.no/index.php/NIK/article/view/437}
}
```

# TODO List
* State autolabeling (Feb?)
* FPS Control
* Docker Support


# Prerequisites
* Linux based operating system (Ubuntu 17.04 and 17.10 are tested)
* Python 3.x.x (3.5 and 3.6 are tested)
* gnash
* xvfb

# Installation

```python
pip install git+https://github.com/UIA-CAIR/FlashRL
```

# Deploy new environment
Setting up a new environment is a relatively simple process. We allow developers to import custom environments through ```project/contrib/environments/```

A typical custom implementation looks like this:
```python
- project
    - __init__.py
    - main.py
    - contrib
        - environments
            - env_name
                - __init__.py
                - dataset.p
                - model.h5
                - env.swf

```
in the following section, we demonstrate how to implement the flash game Mujaffa as an environment for FlashRL.

## Mujaffa-1.6
### Prerequisites
* SWF Game File
* Python 3x
* Keras

### 
*  Create directory structure ```mkdir -p contrib/environments/mujaffa-v1.6```
*  Create Configuration file:  
```python 
echo "define = {
    "swf": "mujaffa.swf",
    "model": "model.h5",
    "dataset": "dataset.p",
    "scenes": [],
    "state_space": (84, 84, 3)
}" > contrib/environments/mujaffa-v1.6/__init__.py
```

* Add swf "mujaffa.swf" to ```contrib/environments/mujaffa-v1.6/```
* Create file ```main.py in project root``` with following template
```
from FlashRL import Game

def on_frame(state, type, vnc):
    # vnc.send_key("a") # Sends the key "a"
    # vnc.send_mouse("Left", (200, 200)) # Left Clicks at x=200, y=200
    # vnc.send_mouse("Right", (200, 200)) # Right Clicks at x=200, y=200
    pass

g = Game("mujaffa-v1.6", fps=10, frame_callback=on_frame, grayscale=True, normalized=True)
```

The game will now run without issues and you can control the game via VNC. The game states are however not identified and must be done manually in the on_frame loop (for now)

### Todos
Document state recognition module



# Tested envrionments
```
* Multitask
* Multitask_2
* 2048

# GYM
Not yet available, but soon!


# Licence
Copyright 2017/2018 Per-Arne Andersen

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
