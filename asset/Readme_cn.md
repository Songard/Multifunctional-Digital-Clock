# 多功能时钟说明文档

组长：李嘉祺

小组成员：张天舒、胡天朔、张镕州、阙铭淏

## 简介

​	在本项目中，我们利用课上学习的知识，通过基本的前端技术，实现了一个**可交互的多功能时钟。**
​	我们的时钟提供了一个通过**SVG绘制**的表盘。提供了**拖动指针**以及手动输入时间两种交互方式，实现了**闹钟、秒表、计时器**等常见功能。
​	此外，作为一个跨时区远程开发的五人小组，我们从自身需求出发，又额外实现了世界时钟以及**设置日期**等功能。

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\1.png" style="zoom:75%;" />

## 功能

- **时钟交互**: 设置和互动式实时时钟界面， 通过拖动时钟的指针和输入等方式设置时间。

- **闹钟**: 设置可自定义的闹钟，支持自定义日期，以及铃声功能。

- **秒表**: 记录经过的时间，支持开始、暂停和复位功能。

- **计时器**: 倒计时功能，设置特定时间长度，到点时会有通知。

- **世界时钟**: 显示全球不同城市的当前时间，以及日夜变化。

  

## 技术栈

- **HTML**: 用于结构化网页内容。

- **CSS**: 用于网页样式和响应式设计。

- **JavaScript**: 用于实现交互功能和时间相关的功能。

  

## 安装和设置

1. 克隆仓库到本地计算机：
   ```bash
   git clone https://github.com/Songard/Multifunctional-Digital-Clock
   ```

2. 进入项目目录：
   ```bash
   cd multi-functional-clock
   ```

3. 在网页浏览器中打开 `index.html` 查看应用程序。

   

## 使用说明和技术原理

### 时钟交互

#### 使用说明

- **默认显示**: 打开 `index.html`，默认进入首页，会自动获取系统时间显示，并自动更新。
- **设置时间**: 在“设置时间”输入框中输入小时、分钟和秒，然后点击“设置时间”按钮。还可以在“设置日期”输入框中输入年月日更改日期。电子时间和钟表指针会进行相应移动。如果输入的时间不合法（例如，小时大于23或分钟大于59），将显示错误消息。
- **恢复当前时间**: 点击“恢复当前时间”按钮，时钟将显示系统的当前时间。
- **指针拖动**:在首页，用鼠标选中时钟的时、分、秒针并拖动，可以根据拖动到的位置，实现时钟时间与数字显示时间的同步更改。在从一日的23:59拖动到后一日的00:00时，或者相反情况下，日期会随之更改（即模拟正常时钟的日期改变）。

#### 技术原理

- **HTML/CSS**: 时钟的布局包括表盘、时针、分针、秒针和数字时间显示。CSS用于样式设置，如时钟大小、颜色和布局。
- **JavaScript**: 
  - 通过 `Date` 对象获取系统的当前时间，并更新时钟和日期显示。
  - 利用 `setInterval` 函数每100毫秒更新一次时钟显示，实现秒针的平滑移动。
  - 添加事件监听器到“设置时间”和“设置日期”按钮，当用户点击时，获取输入框中的值并更新时钟显示。
  - 对时分秒针被按下鼠标的时间添加监听，对应函数 `handleMouseDown(event)`。在其中，监听函数 `moveHandler(event)` 被添加，实时更新当前时钟对应时间；监听函数 `upHandler()` 也被添加，在鼠标抬起时删除自己与 `moveHandler(event)` 的事件监听，恢复为按下前的监听事件列表。
- **SVG绘图**:
  - **表盘绘制**: 使用SVG创建了一个 `<svg>` 元素，并设置了 `viewBox` 属性定义一个虚拟的画布，在其中绘制表盘。并通过设置 `preserveAspectRatio` 属性，确保图形在缩放时保持正确的宽高比。
  - **时钟指针**: 时针、分针和秒针都是使用SVG的 `<line>` 元素绘制的。每个 `<line>` 元素都有其起点和终点，以及颜色和宽度属性，这些属性定义了指针的外观。然后使用 `setAttribute` 方法更新它们的 `transform` 属性来动态地旋转指针。



### 世界时钟

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\2.png" style="zoom:75%;" />

#### 使用说明

- 从 `index.html` 进入“世界时钟”页面，会自动获取默认设置地区的时间并更新。使用下拉选框设置每个钟表所显示的城市，四个钟表可以独立调整。每次设置时间都会根据当前系统时间以及时区来更新相应城市的时间。

#### 技术原理

- **HTML/CSS**: 使用HTML嵌入创建四个时钟的布局，与主时钟基本相同，但为了整体功能清晰有用、页面简洁而去除了拖动指针和设置日期的功能。使用CSS管理每个电子表显示框的样式和排列，并管理嵌入的钟表的位置。
- **SVG绘图**: 给所有时钟的表盘添加了分钟刻度，相对小时刻度较细且较短，符合真实时钟的设计，更加清晰易读。
- **JavaScript**: 使用URL对嵌入的钟表传入时间作为参数，外部页面在每次刷新和重设地区时更新传入参数，内部时钟监听参数改变的事件，在改变时重设时间。这样保证了时钟既能在需要的时候更新，但又不会由于刷新过于频繁而无法有效显示内容。
- **UI优化**: 优化了表盘设计，添加了一个方形框来容纳表盘，并添加阴影进行美化。



### 计时器

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\5.png" style="zoom:75%;" />

#### 使用说明

- 在输入框中输入希望设定的时间，点击“开始”即可开始计时，中途可以暂停和取消。倒计时结束后会响铃提示。最后5秒数字会变红。

#### 技术原理

- **HTML/CSS**: 
  - 使用HTML定义计时器显示区域，输入框和按钮，通过CSS设置文本颜色，当剩余时间小于或等于5秒时，将文本颜色设置为红色。
- **JavaScript**: 
  - 通过添加事件监听器的方式实现按键事件的处理，及时调用相关函数，更改按钮显示等。通过 `setInterval` 每秒减少时间，并调用 `updateTimerDisplay` 更新显示。当时间小于或等于5秒时，改变文本颜色为红色，时间结束时播放音频并弹出提示。并完成重置。



### 秒表

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\4.png" style="zoom:75%;" />

#### 使用说明

- 点击“开始”即可开始计时，计时中点击“暂停”可以暂停计时，点击“记录”则记录当前时间。点击“复位”则归零。

#### 技术原理

- **HTML/CSS**: 
  - 使用HTML定义秒表显示区域，记录的时间显示区域和按钮，通过CSS设置文本颜色和布局。
- **JavaScript**: 
  - 通过添加事件监听器的方式实现按键事件的处理，及时调用相关函数，更改按钮显示等。通过 `setInterval` 开始计时，并定时更新。当检测到“记录”按钮被按下时，将当前的时间以字符串的形式加入到记录时间显示的部分。当检测到按下“暂停”键时终端计时，同时完成按键的变换。当检测到按下“复位”键时则清零，并清除所有记录的时间。



### 闹钟

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\3.png" style="zoom:75%;" />

#### 使用说明

- 设定闹钟时间的方法与时钟部分相同。这里主要介绍闹钟相关功能的使用方法。用户应通过输入框设定时间，之后点击“设置闹钟”，看到提示即代表闹钟设定成功，也可在闹钟到点前点击“取消闹钟”。对于不合理的设定时间（不存在的日期/时间或已经过去的时刻），会有相应的提示，提示内容会以红字显示在提示框中。

#### 技术原理

- **HTML/CSS**: 
  - 闹钟部分的HTML和CSS主要负责输入框、按钮和提示的显示区域。设置相关字体等。
- **JavaScript**: 
  - 通过添加事件监听器的方式实现按键事件的处理，及时调用相关函数。对于用户输入的合法性检查也在这一部分完成。当用户设定闹钟后，通过 `setInterval` 方法定时检查是否到点，到点则响铃提示。关于当前的时间的信息通过 `iframe` 从时钟处获取。当用户点击取消闹钟后，通过 `clearInterval` 的方式终止检查。



### 日期设置

#### 使用说明

- 在“设置日期”按钮左侧输入框中输入年月日（留空的部分分别默认为当年、1月、1日），点击“设置日期”按钮，日期相应变化。若输入日期不合法（如12345年x月x日、2025年2月29日），将显示错误消息，但不影响时钟正常运转。

#### 技术原理

- **JavaScript**

  - 使用默认 `Date` 类，获取系统时间。按下“设置日期”按钮，触发设置时间函数，在检查输入合法性函数 `isValidDate(year, month, day)` 通过后，显示在 `dateDisplay` 元素中。





## 开发成员和贡献

我们小组在开发过程中全程使用Github管理版本，所有人均参与充分，贡献基本均等。以下是每个人的具体职责：

**李嘉祺**

​	职责：设计**项目框架，整合代码**

**张天舒**

​	职责：实现**秒表、计时器、闹钟**功能

**胡天朔**

​	职责：实现**世界时钟**功能，**UI**设计

**张镕州**

​	职责：实现**时钟绘制**及其它时钟**核心功能**

**阙铭淏**

​	职责：实现**指针拖动**和**日期设置**功能



## 参考内容

1. 本项目技术上参考了[web前端攻城狮](https://www.xuetangx.com/course/THU08091000257/21555721)网络课程，及其课件资料。
2. 本项目在开发过程中参考了大语言模型生成的结果，包括但不限于Gpt-4、Copilot等。
3. 在项目答辩结束后，参考老师助教的建议，以及其他小组的优秀设计进行了部分修改。



## 致谢

感谢清华大学软件学院2024Web前端技术实训课程团队的老师、助教以及讲座嘉宾们的指导教学与对我们的项目支持。