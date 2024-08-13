# Multifunctional-Digital-Clock

[CN](asset/Readme_cn.md) | [EN](README.md)

## Introduction

​	This is a team project for the Web Technology Training course (2024 summer) at Tsinghua University. In this project, we implemented a webpage using HTML, CSS, and JS, which has functions such as alarm clock, stopwatch, timer, and world clock.

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\1.png" style="zoom:75%;" />

## Features

- **Clock Interaction**: Set and interact with a real-time clock interface.

- **World Clock**: Display current times in various cities worldwide.

- **Alarm Clock**: Set alarms with customizable tones and snooze options.

- **Stopwatch**: Track elapsed time with start, stop, and reset functions.

- **Timer**: Countdown feature with notifications upon completion.

  

## Technologies Used

- **HTML**: For structuring the webpage content.

- **CSS**: For styling the webpage and ensuring a responsive design.

- **JavaScript**: For implementing interactive features and time-related functionalities.

  

## Installation and Setup

1. Clone the repository to your local machine:

   ```bash
   git clone https://github.com/Songard/Multifunctional-Digital-Clock.git
   ```

2. Navigate to the project directory:

   ```bash
   cd multi-functional-clock
   ```

3. Open `index.html` in your preferred web browser to view the application.

   

## Usage

### Clock Interaction

- **Default Display**: Upon opening `index.html`, the homepage will automatically display the current system time and continuously update.

-  **Pointer Dragging**: On the homepage, users can click and drag the hour, minute, and second hands of the clock to adjust the time. The digital display will update accordingly to reflect the new time set by the user. If the time is dragged from 23:59 to 00:00 (or vice versa), the date will change automatically to simulate the real clock's date change behavior.

- **Set Time**: Enter the desired hours, minutes, and seconds in the "Set Time" input fields, then click the "Set Time" button. You can also change the date by entering the year, month, and day in the "Set Date" fields. The digital time and clock hands will adjust accordingly. If an invalid time is entered (e.g., hours greater than 23 or minutes greater than 59), an error message will be displayed.

- **Restore Current Time**: Click the "Restore Current Time" button to revert the clock to the current system time.

- **Date Setting**: Enter the desired year, month, and day in the input fields to the left of the "Set Date" button (if left empty, they default to the current year, January, and the first day of the month, respectively). Click the "Set Date" button to update the date. If the entered date is invalid (e.g., February 29th on a non-leap year or an excessively large year number), an error message will be displayed, but the clock will continue to function normally.

### World Clock

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\2.png" style="zoom:75%;" />

- From `index.html`, navigate to the "World Clock" page, which will automatically display the time for a default region.
- Use the dropdown menu to set the displayed city for each clock. There are four clocks available, and each can be set independently.
- The time for each selected city will update according to the current system time and the respective timezone.

### Alarm Clock

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\3.png" style="zoom:75%;" />

- Navigate to the "Alarm" tab, set the time, and select your preferred alarm tone.
- Set the desired alarm time using the input fields, then click "Set Alarm." A confirmation message will indicate successful alarm setting. You can cancel the alarm before it triggers. Invalid times (e.g., non-existent dates or past times) will display an error message in red.

### Stopwatch

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\4.png" style="zoom:75%;" />

- From `index.html`, navigate to the "Stopwatch" tab to start, stop, and reset the stopwatch.
- Click "Start" to begin timing. You can pause by clicking "Pause" and record the current time by clicking "Lap." Click "Reset" to clear the stopwatch and recorded times.

### Timer

<img src="C:\Users\15436\Documents\MyPrograms\web\Multifunctional-Digital-Clock\asset\images\5.png" style="zoom:75%;" />

- Set the countdown duration under the "Timer" tab and receive a notification when time is up.
- Enter the desired countdown time in the input field and click "Start" to begin the timer. You can pause or cancel the countdown midway. When the countdown ends, an alarm will sound, and the last 5 seconds will display in red.





## Technical Details

### Clock Interaction

- **HTML/CSS**: The clock's layout includes elements for the dial, hour hand, minute hand, second hand, and digital time display. CSS is used for styling aspects such as clock size, color, and layout.
- **JavaScript**: 
  - Utilizes the `Date` object to fetch and display the current system time, continuously updating the clock and date display.
  - The `setInterval` function is employed to update the clock every 100 milliseconds, ensuring smooth movement of the second hand.
  - Event listeners are added to the "Set Time" and "Set Date" buttons to retrieve user input and update the clock display accordingly.
  - An event listener is attached to the mouse-down event on the clock hands, handled by the function `handleMouseDown(event)`. This function registers additional listeners for mouse movement (`moveHandler(event)`) to update the clock's time in real-time as the user drags the hands and for mouse release (`upHandler()`) to remove the movement listeners and restore the default event listeners.
  - The system's current date and time are fetched using the default `Date` class. Upon clicking the "Set Date" button, the set date function is triggered. Before updating the displayed date, the input is validated using the function `isValidDate(year, month, day)`. If the validation passes, the new date is displayed in the `dateDisplay` element.
- **SVG Drawing**:
  - **Clock Face**: An `<svg>` element is created to represent the clock face, with the `viewBox` attribute defining a virtual canvas for drawing. The `preserveAspectRatio` attribute ensures that the graphics maintain the correct aspect ratio when scaled.
  - **Clock Hands**: The hour, minute, and second hands are drawn using `<line>` elements, with each line's start and end points, color, and width defining its appearance. The `setAttribute` method is used to update their `transform` properties dynamically, allowing the hands to rotate in response to time changes.

### World Clock

- **HTML/CSS**: The layout of the four clocks is created using embedded HTML elements, similar to the main clock, but without the draggable pointer and date setting functionalities for simplicity and clarity. CSS manages the styling and positioning of each digital display box and the embedded clocks.
- **SVG Drawing**: Minute markers are added to the clock faces, thinner and shorter compared to the hour markers, enhancing readability and mirroring real clock designs.
- **JavaScript**: Embedded clocks receive the time via URL parameters, which are updated whenever the page refreshes or a region is reset. An event listener inside the clock component monitors for changes in these parameters and updates the displayed time accordingly. This ensures that the clocks are updated when needed without frequent refreshes that might disrupt the display.
- **UI Optimization**: The clock faces are housed within a square frame for better aesthetics, and shadows are added to enhance the visual appeal.

### Alarm Clock

- HTML/CSS:
  - The clock UI components are reused from the main clock interface. The alarm-specific HTML and CSS focus on input fields, buttons, and notification areas, including font styling and layout.
- JavaScript:
  - Event listeners manage button interactions, validating user input and setting alarms. Upon setting an alarm, a `setInterval` function periodically checks if the alarm time matches the current time (fetched via an iframe from the clock). If the time matches, an alarm sound is played. The alarm check is terminated using `clearInterval` when the user cancels the alarm.

### Stopwatch

- **HTML/CSS**:
  - HTML defines the stopwatch display area, recorded times section, and buttons. CSS manages the layout and text styling.
- **JavaScript**:
  - Event listeners manage button actions, calling functions to start, pause, and reset the stopwatch. The `setInterval` function is used for timing, updating the display periodically. Laps are recorded as strings and displayed in the lap section. The "Pause" button stops the timer, and the "Reset" button clears all recorded times and resets the display.

### Timer

- **HTML/CSS**:

  - HTML defines the timer display area, input fields, and buttons. CSS sets the text color, with the color changing to red when the remaining time is less than or equal to 5 seconds.

- **JavaScript**:

  - Event listeners handle button actions, updating the display and managing state changes. The `setInterval` function decreases the time every second, updating the display using `updateTimerDisplay`. When time runs out, an alarm sound is played, and a notification is shown, followed by a reset.

  

### Development Team and Contributions

- **Li Jiaqi**  
  Responsibilities: Project architecture design, code integration  
  Contribution: Li Jiaqi led the overall design of the project's architecture, ensuring a cohesive structure and flow. Additionally, they were responsible for integrating the various components and code developed by team members into a unified application.

- **Zhang Tianshu**  
  Responsibilities: Implementation of Stopwatch, Timer, and Alarm Clock features  
  Contribution: Zhang Tianshu developed the core functionalities of the Stopwatch, Timer, and Alarm Clock features, including their user interfaces and interactive elements. They ensured the accurate timing mechanisms and user-friendly experiences.

- **Hu Tianshuo**  
  Responsibilities: Implementation of World Clock feature, UI design  
  Contribution: Hu Tianshuo was responsible for developing the World Clock feature, enabling users to view times from different cities. Additionally, they contributed to the overall UI design, enhancing the visual appeal and usability of the application.

- **Zhang Rongzhou**  
  Responsibilities: Implementation of clock drawing and core functionalities  
  Contribution: Zhang Rongzhou worked on the clock's graphical representation and core functionalities, including the SVG-based clock face and hand movements. They ensured that the clock's appearance and behavior were accurate and visually pleasing.

- **Que Minghao**  
  Responsibilities: Implementation of pointer dragging and date setting features  
  Contribution: Que Minghao developed the interactive pointer dragging feature, allowing users to set the time manually. They also implemented the date setting functionality, ensuring seamless synchronization between the digital and analog displays.
  
  

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

We would like to thank the Web Technology Training course instructors at Tsinghua University for their guidance and support throughout this project.

