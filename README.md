
# 📝 Explicação do Código: Cadastro com Arquivo JSON

Este código cria um **sistema de cadastro de pessoas** utilizando **JSON** como formato para armazenar os dados. Os dados são gravados em um arquivo chamado `dados.json`.

---

## 📁 Criação e verificação do arquivo

```python
ARQUIVO = "dados.json"

with open(ARQUIVO, "a+") as arquivo:
    arquivo.seek(0)
    try:
        json.load(arquivo)
    except:
        arquivo.write("[]")
```

### O que faz?
- Garante que o arquivo `dados.json` exista.
- Se o arquivo estiver vazio ou com erro de leitura, ele escreve uma lista vazia `[]` nele.

---

## 📤 Função `carregar()`

```python
def carregar():
    with open(ARQUIVO, "r") as arquivo:
        return json.load(arquivo)
```

### O que faz?
- Abre o arquivo `dados.json` no modo de leitura.
- Lê o conteúdo do JSON e **retorna os dados como uma lista de dicionários**.

---

## 💾 Função `salvar(dados)`

```python
def salvar(dados):
    with open(ARQUIVO, "w") as arquivo:
        json.dump(dados, arquivo)
```

### O que faz?
- Recebe uma lista de dados como parâmetro.
- Abre o arquivo no modo de escrita e **salva os dados no formato JSON**, sobrescrevendo o conteúdo anterior.

---

## 🧑 Função `criar()`

```python
def criar():
    nome = input("Nome: ")
    idade = input("Idade: ")
    email = input("Email: ")
    tel = input("Telefone: ")

    dados = carregar()
    dados.append({"nome": nome, "idade": idade, "email": email, "telefone": tel})
    salvar(dados)
    print("Salvo!")
```

### O que faz?
- Pede ao usuário que informe nome, idade, e-mail e telefone.
- Carrega os dados existentes.
- **Adiciona um novo dicionário com essas informações** na lista.
- Salva a nova lista no arquivo.

---

## 📋 Função `listar()`

```python
def listar():
    dados = carregar()
    for p in dados:
        print(p)
```

### O que faz?
- Carrega os dados do arquivo.
- Percorre cada item e **imprime os cadastros salvos**.

---

## ✏️ Função `atualizar()`

```python
def atualizar():
    nome = input("Nome para atualizar: ")
    dados = carregar()
    for linha in dados:
        if linha["nome"] == nome:
            linha["idade"] = input("Nova idade: ")
            linha["email"] = input("Novo email: ")
            linha["telefone"] = input("Novo telefone: ")
            salvar(dados)
            print("Atualizado!")
            return
    print("Nome não encontrado.")
```

### O que faz?
- Pede o nome da pessoa a ser atualizada.
- Procura essa pessoa na lista de dados.
- Se encontrar, **pede as novas informações** e atualiza o cadastro.
- Salva os dados atualizados no arquivo.

---

## ❌ Função `deletar()`

```python
def deletar():
    nome = input("Nome para deletar: ")
    dados = carregar()
    for linha in dados:
        if linha["nome"] == nome:
            dados.remove(linha)
            salvar(dados)
            print("\n\n ❌ Deletado! \n\n")
            return
    print("Nome não encontrado.")
```

### O que faz?
- Pede o nome da pessoa a ser deletada.
- Procura na lista de dados.
- Se encontrar, **remove o registro dessa pessoa** e salva os dados novamente.

---

## 🧭 Função `menu()`

```python
def menu():
    while True:
        print("\n1 - Criar")
        print("2 - Listar")
        print("3 - Atualizar")
        print("4 - Deletar")
        print("5 - Sair")
        opcao = input("Escolha: ")
        if opcao == "1":
            criar()
        elif opcao == "2":
            listar()
        elif opcao == "3":
            atualizar()
        elif opcao == "4":
            deletar()
        elif opcao == "5":
            break
```

### O que faz?
- Exibe um menu com opções numeradas.
- Chama a função correspondente de acordo com a escolha do usuário.
- Só para quando a opção for "5 - Sair".

---

## 🧠 Questão para os alunos:

### 💡 **Desafio de Fixação**

Você precisa criar um pequeno sistema de **cadastro de contatos**, que permita:

1. **Adicionar** uma nova pessoa (nome, idade, e-mail, telefone).
2. **Listar** todas as pessoas cadastradas.
3. **Atualizar** os dados de uma pessoa existente, procurando pelo nome.
4. **Excluir** uma pessoa do cadastro, também pelo nome.

Use um **arquivo JSON** para armazenar os dados e certifique-se de que:
- Os dados são lidos e gravados corretamente.
- O sistema sempre mostra o menu até que a pessoa escolha "Sair".

💬 *Dica:* Use as funções `carregar`, `salvar`, `criar`, `listar`, `atualizar`, `deletar` e `menu` para estruturar seu sistema.
