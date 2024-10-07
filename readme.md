# Easy Component Hierarchy Overlay (.echo)

other words that can be used in name: easy component simple straightforward hierarchy gui ui layout overlay

alternative names: Straightforward Component UI (.scui)

<br>

```
main: {
	grid: 1x2
	padding: 2
	background image: background.png
	
	top_area: {
		grid: 2x1
		spacing: 2
		
		obj_viewport: {
			3d viewer: true
		}
		
		projects_area: {
			grid: 1x2
			spacing: 2
			column 0: 10 50
			
			projects_controls: {
				grid: 3x1
				spacing: 2
				
				project_selector: {
					border: 1
					items:
				}
				
				add_project_button: {
					border: 1
					text: +
					button: true
				}
				
				remove_project_button: {
					border: 1
					text: -
					button: true
				}
				
			}
			
			project_files: {
				item scroll height: 0.2ph
				grid: 1x0
				
				project_file_item_template: {
					
				}
				
			}
			
		}
		
	}
	
}
```

<br>

### Notes

This works kinda like unity's object and component model, where each GuiElement starts with only a Frame component, and different components are enabled if any their fields are used.

- GuiElement names are snake_case
- most sizes (width, height, border, etc.) should be based off parents' heights

Components:

```
Frame:
margin: [float wh] = 0
margin: [float wh] [float wh]
margin: [float wh] [float wh] [float wh] [float wh]
padding: [float wh] = 0
padding: [float wh] [float wh]
padding: [float wh] [float wh] [float wh] [float wh]
border: [float sh] = 0
border color: [color] = #000000
width: [float ph] = null
height: [float ph] = null
min width: [float wh] = null
min height: [float wh] = null
max width: [float wh] = null
max height: [float wh] = null
aspect ratio: [float] = null
background color: [color]
background image: [file path]
x alignment: ["left" | "right" | "center"] = "center"
y alignment: ["top" | "bottom" | "center"] = "center"
rounding = [float]

Grid:
grid: [int]x[int]
row $: [float] [float] + = 1 1 + // these are ratios, it is convention to try to be based on multiples of 10 (eg 10 50 instead of 1 5)
column $: [float] [float] + = 1 1 +
spacing: [float wh] = padding

Scrollable:
item scroll width: [float pw] = 1
item scroll height: [float wh] = 0.1

Text:
text: [text]
edit text: [bool]
font: [text]
text size: [float wh | "auto"]

Button:
button: true

ComboBox:
items: [string] *

3DViewer:
3d viewer: true
```

Every object has a base type (grid, 3DViewer, etc.). Grid objects can have multiple children (filled left to right, top to bottom), but most other types only allow one child. 

Values tagged with "wh" are in percentages of window height. In actual layout, you can also append ww, wh, pw, ph, sw, sh for percentages of window width, window height, parent width, parent height, screen width, and screen height respectively (e.g. "margin: 2pw" is 2% of parent width).
