# Power-BI-DAX-code-to-show-numbers-in-different-formats-within-the-same-column-

Yesterday, while randomly checking one of my projects, I realized that Power BI’s display units sometimes don’t format numbers properly, which can affect how readable the data is. For example, if you have a bar chart where some numbers are in millions and others are just in hundreds, the default formatting can look messy. So, how do you make sure each value is displayed in the right format?

To solve this, I went through several YouTube tutorials and articles. Most of them suggested using DAX, but none of the codes gave me exactly what I needed. After over an hour of trial and error—plus a little help from ChatGPT, I finally figured out the right way to do it. Here’s how you can apply dynamic display units using DAX:


**Step 1: Create your Measure**

•	Firstly, you will have to create the measure you want to work with

•	For example, If I want to create a measure showing total sale . I will type: 

`Total Sales = SUM('Store'[Amount])`

**Step 2: Change the Format of Your Measure**

•	Next, select your measure and go to “Measure Tools”

•	From there, change the format to “Dynamic”

•	Now, you’ll see separate formula bars for "Measure" and "Format"

•	In the “Format”, type the following code:

          VAR salesMeasure = [Total Sales]
          return
          SWITCH (TRUE(),
          salesMeasure<1000,"0",
          salesMeasure<1000000, "#,.0K",
          salesMeasure<1000000000, "#,,.0M",
          salesMeasure>=1000000000, "#,,,.0B")

You can also add currency and other symbols like this:
          
          VAR salesMeasure = [Total Sales]
          return
          SWITCH (TRUE(),
          salesMeasure<1000,"$0",
          salesMeasure<1000000, "$#,.0K",
          salesMeasure<1000000000, "$#,,.0M",
          salesMeasure>=1000000000, "$#,,,.0B")

**Step 3: Format The Chart**

•	Lastly, select the Chart you want to use, then go to Format > Values and change the “Display Units” from “Auto” to “None”
