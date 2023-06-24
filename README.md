# CSV-populator-GUI
(GUI-using-GTK3-and-Python)
## Problem statement:
  I have a .csv file which has n-columns. A few of these columns are entry_fields while few are drop_down. I will fill the first line of .csv manually, each entry in each column indicating the header for that column, with comma as the separator. As n value increases, and as the number of drop_down options(for drop_down columns) is more, it becomes challenging to make entries without errors (especially if entries into some coloumns are sentences!). The intent of this GUI is to reduce the hassle in filling this .csv. From visual ease pov, consider the below cases <br>
  ```
  case 1: column 1, column 2, column 3, column 4, column 5,column 6, column 7
          entry1,,entry3,,,,entry? 

  case 2: column 1: entry1 
          column 2:        
          column 3: entry3 
          column 4:        
          .                
          .                
          .                
```
  case 1 demos the issue at hand and case 2 shows how a simple GUI can help.

## Action plan:
I break down this task into smaller chunks, write code for each chunk, and finally append all the chunks.
  - [chunk_1 Basic frame](#chunk_1-basic-frame)
  - [chunk_2 Read the csv](#chunk_2-Read-the-csv)
  - [chunk_3 Which rows are entry_field and which are drop_down?](#chunk_3-Which-rows-are-entry_field-and-which-are-drop_down?)
  - [chunk_4 Saving the entries](#chunk_4-saving-the-entries)
  - [chunk_5 Populating the csv with the saved entries](#chunk_5-populating-the-csv-with-the-saved-entries)
  - [chunk_6 Resetting the GUI](#resetting-the-gui)
  - [References](#references)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

### chunk_1 Basic frame
Defining the class name, setting name for the window, defining how big the gui should be, and creating the conatiner form the head. The tail of the code is also written in this step. We create window, terminate the code, and call the main event in the tail part. All other logic lies between head and tail.
```python
#head part starts
import csv
import gi
gi.require_version('Gtk', '3.0')
from gi.repository import Gtk

class csv_populator_gui(Gtk.Window):
    def __init__(stative_boss):
        Gtk.Window.__init__(stative_boss, title="StativeBoss's csv gui")
        stativeboss.set_border_width(0) 
        screen = stativeboss.get_screen()
        window_width = screen.get_width()
        window_height = screen.get_height()
        grid = Gtk.Grid()
        stativeboss.add(grid)
        stativeboss.set_default_size(window_width, window_height)
#head part ends
      
 <this space will be filled with code for core logic as we move through the repo>

#tail part starts
win = csv_populator_gui()
win.connect("destroy", Gtk.main_quit)
win.show_all()
Gtk.main()
#code ends
```
_Explanation_: <br/> 
First, I'm importing csv, and gi libraries. csv library is used to read and write csv files. gi library is imported so that we can further import Gtk library from it. gi.require_version makes sure that the code runs only if installed version is atleast 3.0. If an older version is installed it'll be a RuntimeError. To check which version you have, use 
               ```
               pkg-config --modversion gtk+-3.0
              ```
Next, I'm defining a class called 'csv_populator_gui' which extends from the parent class 'GTK.Window'. It means that csv_populator_gui will inherit all properties and methods of 'GTK.Window'. In def__init__() block we initialize different configuration settings. Here, I am using it to configure the GUI dimensions. It's upto our preference as to what size we want the GUI to be. I prefer the GUI to fit to the screen, so I'm first defining the width as 0 (default), then fetching the dimensions of screen and finally assigning these dimensions to default. 'stative_boss' is the handle for this instance of csv_populator_gui. <br/>

In the tail part, I'm creating a window for the main class. Then I'm connecting the 'destroy' event to Gtk.main_quit() function. It basically means that I want the code to terminate once I close the window. 

### chunk_2 Read the csv
Read csv and store the fields of first row. These are to be used a labels in GUI. Number of filled fields will tell GUI how many columns are there.
### chunk_3 Which rows are entry_field and which are drop_down?
### References:
- https://python-gtk-3-tutorial.readthedocs.io/en/latest/
