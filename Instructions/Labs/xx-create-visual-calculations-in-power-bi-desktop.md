---
lab:
    title: 'Create Visual Calculations in Power BI Desktop'
    module: 'Create Visual Calculations in Power BI Desktop'
---

# Create Visual Calculations in Power BI Desktop

## **Lab story**

In this lab, you'll create visual calculations using Data Analysis Expressions (DAX). 

In this lab you learn how to:

- Create and edit visual calculations
- Use PREVIOUS(), RUNNINGSUM() and MOVINGAVERAGE() functions to create comparison metrics between each fiscal year
- Use the CALCULATE() function to manipulate filter context
- Use Time Intelligence functions

**This lab should take approximately 45 minutes.**

## Get started

To complete this exercise, first open a web browser and enter the following URL to download the zip folder:

`https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst/raw/Main/Allfiles/Labs/xx-create-visual-calculations-in-power-bi-desktop/xx-visual-calculations.zip`

Extract the folder to the **C:\Users\Student\Downloads\xx-visual-calculations** folder.

Open the **xx-Starter-Sales Analysis.pbix** file.

> ***Note**: You can dismiss the sign-in by selecting **Cancel**. Close any other informational windows. Select **Apply Later**, if prompted to apply changes.*

In Power BI Desktop, go to **File > Options and Settings > Options > Preview features**. Select **Visual calculations** and select **OK**. Visual calculations are enabled after Power BI Desktop is restarted.

## Create a bar chart visual

In this task, you’ll create a bar chart showing sales amount and total product cost by fiscal year.

1. In the **Visualizations** pane, select the clustered bar chart visual type.

   ![Picture 01](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image01.png)

1. In the **Data** pane, from inside the **Date** table, drag the **Year** field into the **Y-axis** well/area. 

1. Drag the **Sales** and **Cost** fields from the **Sales** table into the **X-axis** well/area. 

1. Sort the resulting bar chart by **Year** ascending by using the three-dot menu and selecting **Year** followed by **Sort ascending**:

   ![Picture 02](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image02.png)

### Add calculations

In this task, you'll create new visual calculations based on DAX formulas.

1. With the bar chart selected, select **New visual calculation** in the ribbon:

   ![Picture 03](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image03.png)

1. The visual calculations edit window opens. In the formula bar above the visual matrix enter the following expression:

   ```DAX
    Profit = [Sum of Sales] – [Sum of Cost]
   ```

1. Confirm you now see a Profit column on the visual matrix at the bottom of the screen:

   ![Picture 04](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image04.png)

1. Expand the menu under **New visual calculation** and select **Versus previous** from the template options:

   ![Picture 05](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image05.png)

1. In the formula bar, replace the `[Field]` placeholder with `[Profit]` twice and commit the calculation.

1. Select **Running sum** from the templates menu and replace the `[Field]` placeholder with `[Profit]` and commit the calculation.

1. Select **Moving average** from the templates menu and replace the `[Field]` placeholder with `[Profit]` and the `WindowSize` placeholder with 2. You should now have the following set up:

   ![Picture 06](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image06.png)

### Hide fields and finish visual

In this task, you'll hide some of the fields from the visual and turn others into tooltips.

1. Under the **X-axis** well/area, select the visibily icon of the following fields to hide them from the visual:
   - Sum of Sales
   - Sum of Cost
   - Profit

   ![Picture 07](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image07.png)

Notice how the visual matrix is not updated, and the fields and calculations you hid are now no longer shown on the visual.

1. In the **Visualizations** pane, drag **Running sum** and **Moving average** to the **Tooltips** well/area.  

1. Confirm the visual now meets the goals. Exit out of the visual calculations edit screen to your report:

   ![Picture 08](Linked_image_Files/xx-create-visual-calculations-in-power-bi-desktop_image08.png)

## Create a matrix visual

1. In **Report view**, create a new report page.

1. On **Page 2**, add a matrix visual.

1. Add the following fields to the visual wells/areas:

     - Rows: **Product \| Category**
     - Columns: **Date \| Year**
     - Values: **Sales \| Sales**

 > *The labs use a shorthand notation to reference a field. It will look like this: **Date \| Year**. In this example, **Date** is the table name and **Year** is the field name.*

### Add calculations

1. With the matrix selected, select **New visual calculation** in the ribbon.

1. In the visual calculations edit window, type and save the following calculation: 

   ```DAX
    Versus first = [Sales] - FIRST([Sales])
   ```

Notice how the matrix shows the difference in sales amount for each category versus the first category.

1. Select the field **Versus first** in the **Values** well/area and update your calculation by adding the ROWS value for the Axis parameter to FIRST: 

   ```DAX
    Versus first = [Sales] - FIRST([Sales], ROWS)
   ```

Notice how nothing changes as ROWS is the default value for the Axis parameter. 

1. Replace ROWS with COLUMNS and observe that the calculation now compares the sales amount per category against the first fiscal year.

1. Exit out of the visual calculations edit screen to your report.

## Create a line chart visual
