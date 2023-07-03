# Checklist

### Introduction

The checklist is the set of activities which are there to perform on completion of a task to ensure the fullness and quality of the task.

### Data Types

The data type is an attribute of data, a particular kind of data item, as defined by the values it can take, the computer system used, or the operations that can be performed on it. In order to help to fill in the right kind of data for a data field/ column in Excel, the below-given table has different data types with its description.

<table><thead><tr><th width="150.33333333333331">S.No.</th><th width="186">Data Type</th><th>Definition/Description</th></tr></thead><tbody><tr><td>1</td><td>Alphanumeric</td><td>It contains alphabets and numbers. And generally used to define the code</td></tr><tr><td>2</td><td>Decimal</td><td>Floating point number with a fraction value up to 2 decimal places</td></tr><tr><td>3</td><td>Integer</td><td>Whole number without having a fraction part in it</td></tr><tr><td>4</td><td>Text</td><td>A string of alphabets, numbers, spaces, and symbols</td></tr><tr><td>5</td><td>Date</td><td>It represents a date and is captured in the format of ‘DD/MM/YYYY’</td></tr><tr><td>6</td><td>Reference</td><td>It is a code of a record from the referred entity and having a related record in the prevailing entity</td></tr><tr><td>7</td><td>Document</td><td>It represents a document which is needed as an attachment with other relevant details in the template</td></tr></tbody></table>

### Checklist

#### **State Level: These activities are applicable to state-level entities only**

<table><thead><tr><th width="97.33333333333331">Sr. No.</th><th width="467">Activity</th><th>Example</th></tr></thead><tbody><tr><td>1</td><td>The entity is to be decided to be defined at the state level and all the ULBs are agreed on the same.</td><td>NA</td></tr><tr><td>2</td><td>Data filled into templates should cater to the needs of each and every ULBs.</td><td>NA</td></tr></tbody></table>

#### **General: These activities are applicable to all the entities**

<table><thead><tr><th width="113.33333333333331">Sr. No.</th><th width="435">Activity</th><th>Example</th></tr></thead><tbody><tr><td>3</td><td>Order of headers should remain unchanged in the template while filling the data.</td><td>NA</td></tr><tr><td>4</td><td>Value filled into the template doesn’t exceed the given data size limit.</td><td>NA</td></tr><tr><td>5</td><td>Codes filled in the template for all the records are unique. It means no 2 records in the template share the same code.</td><td><p>Below records in code, value pair is not acceptable.</p><p>RES - Residential</p><p>RES - Non-residential</p></td></tr><tr><td>6</td><td>All the columns marked with an asterisk must be filled with the values and not even a single record left without a value.</td><td>NA</td></tr><tr><td>7</td><td>Reference value in the template must also exist in the referred entity template. A value without being present in the referred entity template is invalid.</td><td>NA</td></tr><tr><td>8</td><td>None of the values filled in the template should have a character which is not allowed.</td><td>NA</td></tr><tr><td>9</td><td>Mobile Numbers filled into the template must be 10 digit valid mobile numbers without country code.</td><td>NA</td></tr><tr><td>10</td><td>Email id filled into template should be a valid email ID.</td><td>NA</td></tr><tr><td>11</td><td>Local language values should be Unicode charset only.</td><td>NA</td></tr></tbody></table>

#### **Data Type Based: These activities are applicable to all entities**

<table><thead><tr><th width="121.33333333333331">S.No.</th><th width="444">Activity</th><th>Example</th></tr></thead><tbody><tr><td>12</td><td>Values of data type alphanumeric consist of the alphabet and numeric values only. All the entity code should follow this.</td><td><p>Allowed - ABC01</p><p>Not allowed - ABC#01</p></td></tr><tr><td>13</td><td>Values of data type decimal must be a number having fraction part up to 2 places of decimal.</td><td><p>Allowed - 23.87</p><p>Not allowed - 12.0982</p></td></tr><tr><td>14</td><td>Values of data type integer must be a number which is not a fraction but a whole number.</td><td><p>Allowed - 15</p><p>Not allowed - 12.01</p></td></tr><tr><td>15</td><td>Values of data type text must be a string of alphabets, numbers, special characters, and spaces.</td><td>NA</td></tr><tr><td>16</td><td>Values of data type date must be a date in the format ‘DD/MM/YYYY’. Here DD means day, MM means month and YYYY means years.</td><td><p>Allowed - 31/12/2019</p><p>Not allowed - 12/31/2019, 31/12/19, etc.</p></td></tr><tr><td>17</td><td>Values of data type reference must be a reference to another entity referring to a value in that entity. Only the code of the referred record from the referred entity is provided as a value here.</td><td>NA</td></tr><tr><td>18</td><td>Value of the data type document must be a document which is to be provided separately as an attachment while submitting the data along with a filled data template.</td><td>NA</td></tr></tbody></table>

