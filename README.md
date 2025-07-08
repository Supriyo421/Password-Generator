import tkinter as tk
from tkinter import messagebox
import random
import string

# Function to generate password
def generate_password():
    try:
        length = int(length_entry.get())
    except ValueError:
        messagebox.showerror("Error", "Please enter a valid number.")
        return

    use_letters = letters_var.get()
    use_numbers = numbers_var.get()
    use_symbols = symbols_var.get()

    characters = ""

    if use_letters:
        characters += string.ascii_letters
    if use_numbers:
        characters += string.digits
    if use_symbols:
        characters += string.punctuation

    if not characters:
        messagebox.showerror("Error", "Select at least one character type.")
        return

    password = ''.join(random.choice(characters) for _ in range(length))
    result_label.config(text="Generated Password:\n" + password)

# GUI setup
root = tk.Tk()
root.title("Password Generator")
#root.geometry("300x300")
#root.resizable(False, False)

# Widgets
tk.Label(root, text="Enter Password Length:").pack(pady=5)
length_entry = tk.Entry(root)
length_entry.pack(pady=5)

letters_var = tk.BooleanVar(value=True)
numbers_var = tk.BooleanVar(value=True)
symbols_var = tk.BooleanVar(value=True)

tk.Checkbutton(root, text="Include Letters", variable=letters_var).pack(anchor='w', padx=20)
tk.Checkbutton(root, text="Include Numbers", variable=numbers_var).pack(anchor='w', padx=20)
tk.Checkbutton(root, text="Include Symbols", variable=symbols_var).pack(anchor='w', padx=20)

tk.Button(root, text="Generate Password", command=generate_password).pack(pady=10)

result_label = tk.Label(root, text="", fg="blue", wraplength=280)
result_label.pack(pady=10)

# Run the GUI loop
root.mainloop()
