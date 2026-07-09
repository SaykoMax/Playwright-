Based on the bugs you actually found during testing, here they are in a professional defect report format.


---

BUG-001: Clear button is disabled when the "Your Colors" table is empty

Subject: Clear button cannot be clicked when the "Your Colors" table is empty.

Steps to Reproduce:

1. Launch the Paint Mixer application.


2. Ensure no color mixes have been created.


3. Observe the Clear button.



Expected Output: The Clear button should either remain enabled and perform no action or provide appropriate feedback to the user.

Actual Output: The Clear button is disabled and cannot be clicked when the table is empty.


---

BUG-002: Mix button cannot be used again for the same color ratio

Subject: Mix button becomes unavailable for the same Blue and Green ratio.

Steps to Reproduce:

1. Set Blue = 2 and Green = 3.


2. Click the Mix button.


3. Without changing the values, click the Mix button again.



Expected Output: The application should allow creating the same mix again or display an appropriate validation message explaining why it is not allowed.

Actual Output: The Mix button cannot be used again for the same color ratio without any explanation.


---

BUG-003: Sort functionality does not indicate sorting order

Subject: Sort feature does not specify whether records are sorted in ascending or descending order.

Steps to Reproduce:

1. Create multiple paint mixes with different Blue and Green ratios.


2. Click the Sort button.


3. Observe the order of the records.



Expected Output: The application should indicate the sorting order (Ascending/Descending) or provide an option to choose the sorting direction.

Actual Output: Records are sorted, but the sorting order is not specified, causing ambiguity for the user.


---

BUG-004: Mixed color entries do not display a shade/color label

Subject: No label is displayed for the generated shade of color.

Steps to Reproduce:

1. Select valid Blue and Green quantities.


2. Click the Mix button.


3. Observe the generated entry in the Your Colors table.



Expected Output: The generated color should display an appropriate shade/color name or label in the Color column.

Actual Output: The generated shade is displayed without any descriptive color label.


---

These are based on your observations and are appropriate for a QA training submission. If your mentor expects Redmine-style reports, you can also add Severity (Low/Medium/High), Priority, and Status columns.
