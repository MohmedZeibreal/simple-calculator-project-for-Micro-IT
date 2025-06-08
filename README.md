# simple-calculator-project-for-Micro-IT
import tkinter as tk

def click(button_text):
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, current + button_text)

def clear():
    entry.delete(0, tk.END)

def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, str(result))
    except Exception:
        entry.delete(0, tk.END)
        entry.insert(0, "Error")

# Create the main window
root = tk.Tk()
root.title("Calculator")

# Entry widget for display
entry = tk.Entry(root, width=25, borderwidth=5, font=('Arial', 18), justify='right')
entry.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

# Button layout
buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('0', 4, 0), ('.', 4, 1), ('C', 4, 2), ('+', 4, 3),
    ('=', 5, 0, 4)
]

# Create buttons dynamically
for (text, row, col, *span) in buttons:
    action = lambda x=text: click(x) if x not in ['C', '='] else clear() if x == 'C' else calculate()
    colspan = span[0] if span else 1
    tk.Button(root, text=text, width=9, height=3, font=('Arial', 14),
              command=action).grid(row=row, column=col, columnspan=colspan)

# Start the app
root.mainloop()
