# Calculadora_Avancada
import tkinter as tk
from math import sqrt, sin, cos, tan, log, radians, degrees

class Calculadora:
    def __init__(self, root):
        self.root = root
        self.root.title("Calculadora Avançada")

        self.result_var = tk.StringVar()
        self.result_var.set("0")

        self.entry = tk.Entry(root, textvariable=self.result_var, font=("Helvetica", 20), justify="right")
        self.entry.grid(row=0, column=0, columnspan=4)

        botoes = [
            ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
            ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3),
            ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3),
            ("0", 4, 0), (".", 4, 1), ("=", 4, 2), ("+", 4, 3),
            ("raiz", 5, 0), ("sen", 5, 1), ("cos", 5, 2), ("tan", 5, 3),
            ("log", 6, 0), ("exp", 6, 1), ("^", 6, 2), ("Limpar", 6, 3),
            ("comprimento", 7, 0), ("massa", 7, 1), ("tempo", 7, 2), ("°->rad", 7, 3),
        ]

        for texto_botao, linha, coluna in botoes:
            self.criar_botao(texto_botao, linha, coluna)

    def criar_botao(self, texto, linha, coluna):
        botao = tk.Button(self.root, text=texto, font=("Helvetica", 15), command=lambda t=texto: self.ao_clicar_botao(t))
        botao.grid(row=linha, column=coluna, padx=10, pady=10)

    def ao_clicar_botao(self, texto_botao):
        if texto_botao == "=":
            try:
                resultado = eval(self.result_var.get())
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        elif texto_botao == "Limpar":
            self.result_var.set("0")
        elif texto_botao == "raiz":
            try:
                resultado = sqrt(float(self.result_var.get()))
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        elif texto_botao in ["sen", "cos", "tan"]:
            try:
                angulo = radians(float(self.result_var.get()))
                if texto_botao == "sen":
                    resultado = sin(angulo)
                elif texto_botao == "cos":
                    resultado = cos(angulo)
                else:
                    resultado = tan(angulo)
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        elif texto_botao == "log":
            try:
                resultado = log(float(self.result_var.get()))
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        elif texto_botao == "exp":
            try:
                resultado = 2.718 ** float(self.result_var.get())
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        elif texto_botao == "^":
            try:
                base, expoente = map(float, self.result_var.get().split('^'))
                resultado = base ** expoente
                self.result_var.set(resultado)
            except:
                self.result_var.set("Erro")
        # Adicione outras funcionalidades aqui (conversões de unidades, etc.)
        else:
            texto_atual = self.result_var.get()
            if texto_atual == "0":
                self.result_var.set(texto_botao)
            else:
                self.result_var.set(texto_atual + texto_botao)

def main():
    root = tk.Tk()
    calculadora = Calculadora(root)
    root.mainloop()

if __name__ == "__main__":
    main()
