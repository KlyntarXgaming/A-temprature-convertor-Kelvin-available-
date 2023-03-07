```
#! Copyright © GG, Inc. and its affiliates.
import tkinter as tk
from tkinter import ttk
import os
cmd = 'pyinstaller --noconsole index.py'
os.system(cmd)

def convert_temp():
    try:
        temp = float(entry_temp.get())
        unit = str(combobox_unit.get())
        
        if unit == 'Celsius':
            result = (temp * 9/5) + 32
            fahrenheit = round(result, 2)
            kelvin = round(temp + 273.15, 2)
            
            result_label.configure(text=f"{temp}°C is equal to {fahrenheit}°F and {kelvin}K")
        elif unit == 'Fahrenheit':
            result = (temp - 32) * 5/9
            celsius = round(result, 2)
            kelvin = round((temp - 32) * 5/9 + 273.15, 2)
            
            result_label.configure(text=f"{temp}°F is equal to {celsius}°C and {kelvin}K")
        elif unit == 'Kelvin':
            result = temp - 273.15
            celsius = round(result, 2)
            fahrenheit = round((temp - 273.15) * 9/5 + 32, 2)
            
            result_label.configure(text=f"{temp}K is equal to {celsius}°C and {fahrenheit}°F")
    except ValueError:
        result_label.configure(text='Error: Invalid input')

root = tk.Tk()
root.configure(bg='#2c2c2c')
root.geometry("450x250")
root.title("Temperature Converter")
root.iconbitmap('images/224264425_652953542467427_1399419786626747548_n.jpg')
colors = ['#d9eef3', '#a6d8e6', '#6ec1cc', '#29b0b9', '#f5cac3', '#f5a683', '#f57f17', '#f5d63d', '#e5e5e5', '#c5c5c5', '#a5a5a5', '#858585', '#f8e1a3', '#f5b349', '#ed8b00', '#d64200', '#f1e3dd', '#d0b095', '#af7d5a', '#8e4b20', '#d3d3d3', '#a9a9a9', '#808080', '#696969']

color_index = 0

def animate_background():
    global color_index
    bg_color = colors[color_index]
    root.configure(bg=bg_color)
    color_index = (color_index + 1) % len(colors)
    root.after(500, animate_background)

# Start the animation
root.after(0, animate_background)

temp_frame = ttk.Frame(root, padding=10)
temp_frame.pack(pady=20)

entry_temp = ttk.Entry(temp_frame, width=15, font=("Helvetica", 20))
entry_temp.grid(row=0, column=0)

combobox_values = ['Celsius', 'Fahrenheit', 'Kelvin']
combobox_unit = ttk.Combobox(temp_frame, values=combobox_values, state='readonly', font=("Helvetica", 20))
combobox_unit.grid(row=0, column=1)
combobox_unit.current(0)

convert_button = ttk.Button(temp_frame, text='Convert', command=convert_temp, padding=5)
convert_button.grid(row=1, columnspan=2, pady=20)

result_frame = ttk.Frame(root, padding=10)
result_frame.pack()

result_label = ttk.Label(result_frame, text='', font=("Helvetica", 20), foreground='white', background='#2c2c2c')
result_label.pack()
result_label.grid(row=3, columnspan=2)

root.mainloop()
root.bind('<Return>', convert_temp)

# Author: KlyntarX
```
