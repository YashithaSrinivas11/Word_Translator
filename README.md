from tkinter import *
from tkinter import ttk
from deep_translator import GoogleTranslator
from googletrans import LANGUAGES

LANGUAGE_CODES = {value.lower(): key for key, value in LANGUAGES.items()}

def change(text="type", src="English", dest="Kannada"):
    src_code = LANGUAGE_CODES.get(src.lower())
    dest_code = LANGUAGE_CODES.get(dest.lower())
    if src_code and dest_code:
        try:
            trans1 = GoogleTranslator(source=src_code, target=dest_code).translate(text)
            return trans1
        except Exception as e:
            return f"Translation error: {e}"
    else:
        return "Translation error: Invalid source or destination language."

def data():
    s = comb_sor.get()
    d = comb_dest.get()
    masg = Sor_txt.get(1.0, END)
    textget = change(text=masg, src=s, dest=d)
    dest_txt.delete(1.0, END)
    dest_txt.insert(END, textget)

root = Tk()
root.title("Word Translator")
root.geometry("500x700")
root.config(bg='White')

lab_text = Label(root, text="Word Translator", font=("Arial Black", 20, "bold"), bg='White')
lab_text.place(x=100, y=20, height=50, width=300)

frame = Frame(root, bg='White')
frame.pack(side=BOTTOM)

lab_sor_txt = Label(root, text="Source Text", font=("Arial Black", 15, "bold"), bg='White')
lab_sor_txt.place(x=10, y=80, height=30, width=150)
Sor_txt = Text(root, font=("Arial", 15), wrap=WORD)
Sor_txt.place(x=10, y=120, height=200, width=480)

list_text = list(LANGUAGES.values())

comb_sor = ttk.Combobox(root, value=list_text)
comb_sor.place(x=10, y=330, height=40, width=150)
comb_sor.set("English")

button_change = Button(root, text="Translate", relief=RAISED, command=data)
button_change.place(x=170, y=330, height=40, width=150)

comb_dest = ttk.Combobox(root, value=list_text)
comb_dest.place(x=330, y=330, height=40, width=150)
comb_dest.set("Kannada")

lab_dest_txt = Label(root, text="Destination Text", font=("Arial Black", 15, "bold"), bg='White')
lab_dest_txt.place(x=10, y=380, height=30, width=180)
dest_txt = Text(root, font=("Arial", 15), wrap=WORD)
dest_txt.place(x=10, y=420, height=200, width=480)

root.mainloop()
