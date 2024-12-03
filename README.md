# Tópicos
### [Pré-requisitos](#pré-requisitos)
### [Extrair questões do ENEM](#extrair-questões-do-enem)
### [Extrair questõe da Fatec](#extrair-questões-da-fatec)

<br>
<br>

# Pré requisitos

## Python
Ter o python instalado. Veja [Python Download](https://www.python.org/downloads/) para as instruções de instalação.

## Conta Google (para o Gemini AI)
Efetuar o [login em sua conta](https://support.google.com/mail/answer/8494) ou [criar uma nova conta](https://support.google.com/mail/answer/56256)

# Extrair questões do ENEM
Existem duas formas de extrair as questões do Enem.
- A primeira forma é utilizando a própria [API do ENEM](https://github.com/yunger7/enem-api) de forma online. Uma dos problemas é o limite de requisição existente, portanto essa forma será mais lenta.
- A segunda maneira é fazer um self-hosting, o que e remover o limite de requisição manualmente.

> [!WARNING]
> Algumas questões não estão disponíveis pela API do ENEM. Estas serão informadas no Prompt de Comando que estiver executando o servidor da API.

## Extraindo questões usando a API Online
1. No arquivo `enem_extract_questions.py` (/vestibulares/enem), **substitua** todos `urlSelfHosting` por `urlWebsite`.
2. Ainda no mesmo arquivo, no final do código, **descomente** o seguinte block de código:
```python
# Espaçamento para facilitar leitura do console
    print("\n")



    # Espera 10 segundos a cada 10 iterações
    if i % 10 == 0:
        print("\n\nAGUARDA 10 SEGUNDOS PARA NÃO ESTOURAR O LIMITE DE REQUISIÇÕES!\n\n\n")
        time.sleep(10)
```
3. Na pasta root do projeto `vestibular-extrair-questoes`, execute o seguinte comando:
```cmd
py enem.py
```

## Extraindo questões usando o Self-Hosting
1. Faça o [Deploy Rápido](https://docs.enem.dev/self-hosting#deploy-rapido) da API do Enem.
2. **Pare a execução** do servidor e acesse o arquivo `rate-limit.ts` (/lib/api).
Modifique a seguinte linha:
```typescript
this.maxRequests = maxRequests || 10;
```
Para o comando:
```typescript
this.maxRequests = 10000;
```
3. Starte o servidor da API do Enem novamente.
4. Na pasta root do projeto `vestibular-extrair-questoes`, execute o seguinte comando:
```cmd
py enem.py
```


# Extrair questões da FATEC
> [!CAUTION]
> O Gemini AI tende a errar os valores dos campos `enunciado` e `pergunta`. Por isso, é bom revisá-los!

> [!IMPORTANT]
> Nenhum imagem é extraída, estas devem ser feitas manualmente.

1. As questões do Vestibular FATEC serão extraidas usando o [Gemini AI](https://gemini.google.com/) da Google. Para isso, você deve [**criar uma chave de API**](https://aistudio.google.com/apikey) gratuitamente, além de ter uma [conta Google](#conta-google-para-o-gemini-ai).
2. Copie sua API Key do Gemini AI e cole no arquivo `gemini-api-key.txt`
3. Na pasta root do projeto `vestibular-extrair-questoes`, execute o seguinte comando:
```cmd
git update-index --assume-unchanged gemini-api-key.txt
```
4. E em seguida:
```cmd
py fatec.py
```