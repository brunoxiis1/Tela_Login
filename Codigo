import customtkinter as ctk
from tkinter import *
import sqlite3
from tkinter import messagebox

janela = ctk.CTk()

class BackEnd():
    def __init__(self):
        self.conecta_db()
        self.cria_tabela()

    def conecta_db(self):
        self.conn = sqlite3.connect('SistemaLogin.db')
        self.cursor = self.conn.cursor()
        print('Banco de Dados CONECTADO!')

    def desconecta_db(self):
        self.conn.close()
        print('Banco de Dados DESCONECTADO!')

    def cria_tabela(self):
        self.cursor.execute('''
            CREATE TABLE IF NOT EXISTS Usuarios(
            Id INTEGER PRIMARY KEY AUTOINCREMENT,
            Username TEXT NOT NULL,
            Email TEXT NOT NULL,
            Senha TEXT NOT NULL,
            Confirma_Senha TEXT NOT NULL
            );
        ''')
        self.conn.commit()
        print('Tabela criada com sucesso!')


    def cadastrar_usuario(self):
        self.username_cadastro = self.username_entry.get()
        self.email_cadastro = self.email_entry.get()
        self.senha_cadastro = self.password_entry.get()
        self.confirma_senha_cadastro = self.cPassword_entry.get()

        self.conecta_db()

        self.cursor.execute("""
            INSERT INTO Usuarios(Username, Email, Senha, Confirma_Senha)
            VALUES (?, ?, ?, ?)
            """, (self.username_cadastro, self.email_cadastro, self.senha_cadastro, self.confirma_senha_cadastro))

        try:
            if (self.username_cadastro == '' or self.email_cadastro == ''
                    or self.senha_cadastro == '' or self.confirma_senha_cadastro == ''):
                messagebox.showerror(title='Sistema de Login', message='ERRO!\nPor favor preencha todos os campos!')
            elif (len(self.username_cadastro) < 4):
                messagebox.showwarning(title='Sistema de Login', message='ATENÇÃO!\nO nome de usuário deve conter pelo menos 4 caracteres!')
            elif (len(self.senha_cadastro) < 4):
                messagebox.showerror(title='Sistema de Login', message='ERRO!\nA senha deve conter pelo menos 4 caracteres!')
            elif (self.senha_cadastro != self.confirma_senha_cadastro):
                messagebox.showerror(title='Sistema de Login', message='ERRO!\nAs senhas não conferem!')
            else:
                self.conn.commit()
                messagebox.showinfo(title='Sistema de Login', message=f'Parabéns {self.username_cadastro}\nCadastro concluido!')
                self.desconecta_db()
                self.limpa_entry_cadastro()
        except:
            messagebox.showerror(title='Sistema de Login', message='Erro no processamento dos dados!\nPor Favor tente novamente!')
            self.desconecta_db()

    def verifica_login(self):
        self.username_login = self.username_login_entry.get()
        self.senha_login = self.senha_login_entry.get()

        print(self.username_login, self.senha_login)



class Application(BackEnd):
    def __init__(self):
        super().__init__()
        self.janela = janela
        self.tema()
        self.tela()
        self.username_entry = None
        self.email_entry = None
        self.password_entry = None
        self.cPassword_entry = None
        self.tela_login()
        self.cria_tabela()
        janela.mainloop()

    def tema(self):
        ctk.set_appearance_mode('dark')
        ctk.set_default_color_theme('dark-blue')

    def tela(self):
        janela.geometry('700x400')
        janela.title('Sistema de Login')
        janela.iconbitmap('iconlogin.ico')
        janela.resizable(False, False)

    def tela_login(self):
        img = PhotoImage(file='log.png')
        label_img = ctk.CTkLabel(master=janela, image=img, text=None)
        label_img.place(x=25, y=20)

        title_label = ctk.CTkLabel(master=janela, text='Faça o Login para acessar o Sistema!', font=('Roboto', 16, 'bold'), text_color='#00a2ff').place(x=25, y=5)

        login_frame = ctk.CTkFrame(master=janela, width=350, height=396)
        login_frame.pack(side=RIGHT)

        label = ctk.CTkLabel(master=login_frame, text='Sistema de Login', font=('Roboto', 20, 'bold'), text_color=('white'))
        label.place(x=93, y=35)

        self.username_entry = ctk.CTkEntry(master=login_frame, placeholder_text='Nome de Usuário', width=300, font=('Roboto', 14))
        self.username_entry.place(x=25, y=105)
        username_label = ctk.CTkLabel(master=login_frame, text='*O campo nome de usuário é de carácter obrigatório.',
                                       text_color='green', font=('Roboto', 12)).place(x=25, y=135)

        self.password_entry = ctk.CTkEntry(master=login_frame, placeholder_text='Senha de Usuário', width=300, font=('Roboto', 14), show='*')
        self.password_entry.place(x=25, y=175)
        password_label = ctk.CTkLabel(master=login_frame, text='*O campo senha é obrigatório.',
                                       text_color='green', font=('Roboto', 12)).place(x=25, y=205)

        checkbox = ctk.CTkCheckBox(master=login_frame, text='Lembrar-se do Login.').place(x=25, y=235)

        login_button = ctk.CTkButton(master=login_frame, text='LOGIN', width=300, command=self.verifica_login).place(x=25, y=285)

        def tela_register():
            login_frame.pack_forget()

            rg_frame = ctk.CTkFrame(master=janela, width=350, height=396)
            rg_frame.pack(side=RIGHT)

            label = ctk.CTkLabel(master=rg_frame, text='Faça seu Cadastro', font=('Roboto', 20, 'bold'),
                                 text_color=('white'))
            label.place(x=93, y=35)

            span = ctk.CTkLabel(master=rg_frame, text='*Preencha todos os campos corretamente', text_color='green', font=('Roboto', 12)).place(x=25, y=70)

            self.username_entry = ctk.CTkEntry(master=rg_frame, placeholder_text='Nome de Usuário', width=300, font=('Roboto', 14))
            self.username_entry.place(x=25, y=105)

            self.email_entry = ctk.CTkEntry(master=rg_frame, placeholder_text='E-mail do Usuário', width=300, font=('Roboto', 14))
            self.email_entry.place(x=25, y=145)

            self.password_entry = ctk.CTkEntry(master=rg_frame, placeholder_text='Senha do Usuário', width=300, font=('Roboto', 14), show='*')
            self.password_entry.place(x=25, y=185)

            self.cPassword_entry = ctk.CTkEntry(master=rg_frame, placeholder_text='Reoita a Senha', width=300, font=('Roboto', 14), show='*')
            self.cPassword_entry.place(x=25, y=225)

            checkbox = ctk.CTkCheckBox(master=rg_frame, text='Aceitar Termos e Política').place(x=25, y=265)

            def back():
                rg_frame.pack_forget()

                login_frame.pack(side=RIGHT)

            voltar_button = ctk.CTkButton(master=rg_frame, text='Voltar', width=145, fg_color='#525252', command=back).place(x=25, y=325)

            save_button = ctk.CTkButton(master=rg_frame, text='Registrar', width=145, fg_color='green', command=self.cadastrar_usuario).place(x=180, y=325)

        registrar_button = ctk.CTkButton(master=login_frame, text='Cadastre-se', width=125, fg_color='green', hover_color='#91f786', command=tela_register).place(x=200, y=325)
        registrar_label = ctk.CTkLabel(master=login_frame, text='*Não tem conta? registre-se', font=('Roboto', 12), text_color='green').place(x=25, y=325)

    def limpa_entry_cadastro(self):
        self.username_entry.delete(0, END)
        self.email_entry.delete(0, END)
        self.password_entry.delete(0, END)
        self.cPassword_entry.delete(0, END)

    def limpa_entry_login(self):
        self.username_entry.delete(0, END)
        self.password_entry.delete(0, END)

Application()
