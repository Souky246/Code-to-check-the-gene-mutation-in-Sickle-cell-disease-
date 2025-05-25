# Code to detect gene mutation-in-Sickle-cell-disease with interface
import tkinter
# Function to detect mutations or process sequences
def detecter_mutation():
    # Get sequences from the Entry widget
    input_text = sequences.get()
    try:
        sequences_list = [seq.strip()for seq in input_text.upper().split(',')]
        output = ""
        for seq in sequences_list:
            if len(seq) >= 6:
                second_triplet = seq[3:6]
                if second_triplet in ["GAG", "GAA"]:
                    output += f"{seq} \n-> Pas de mutation : Glutamate -> Normal.\n"
                elif second_triplet in ["GTT", "GTA", "GTC", "GTG"]:
                    output += f"{seq} \n-> Mutation détectée : Glutamate remplacé par Valine -> Drépanocytose.\n"
                else:
                    output += f"{seq}\n -> Triplet inattendu.\n"
            else:
                output += f"{seq} \n-> Séquence trop courte pour l'analyse.\n"
        # Update the result_label with the output
        result_label.config(text=output+"\n Analyse terminée!", fg="green", justify="left", anchor="w")

    except Exception as e:
        result_label.config(text=f"Erreur: {str(e)}", fg="red")
# Create Window
Window = tkinter.Tk()
Window.title("DrepaCheck")
Window.geometry("800x500")  # Adjust the size of the window

# Label for instructions
label = tkinter.Label(Window, text='Saisissez vos séquences (séparées par des virgules) :', font='Arial 14 bold', fg='red')
label.grid(row=0, column=0, columnspan=2, pady=10, padx=10)

# Input field
sequences = tkinter.Entry(Window, font='Arial 14', width=50)
sequences.grid(row=1, column=0, columnspan=2, pady=10, padx=10)

# Analyze button
but1 = tkinter.Button(Window, text='Analyser', font='Arial 14', command=detecter_mutation, bg="yellow")
but1.grid(row=2, column=1, pady=10)

# Results display area
result_label = tkinter.Label(Window, text='Résultat : ', font='Arial 14 bold', fg="green", wraplength=700)
result_label.grid(row=3, column=0, columnspan=2, pady=10)

# Adding an image
photo = tkinter.PhotoImage(file="drépano.png")
Image_right = tkinter.Label(Window, image=photo)
Image_right.grid(row=7, column=1, rowspan=1, padx=10)



# Messages to display
msg = tkinter.Label(Window,
    text="Master Medbiotech : Biomedical – FMP Rabat ",
    bg='yellow', font=('Arial', 12), wraplength=800, justify="left")
msg.grid(row=5, column=0, columnspan=2, pady=10, padx=10)

Label1 = tkinter.Label(Window,
		 text="Bienvenue dans DrepaCheck, votre application d'analyse des séquences d'ADN pour la détection des mutations associées à la drépanocytose.",
		 fg = "white", 
                 bg = "red",
		 font = "Times")
Label1.grid(row=4, column=0, columnspan=2, pady=10, padx=10)

# Launching the interface
Window.mainloop()
