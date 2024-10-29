# Alura
catalogo-de-filmes/
├── filmes_catalogo.py
├── filmes.json
└── README.md
# filmes_catalogo.py
import json
import os

# Função para carregar filmes do arquivo JSON
def carregar_filmes():
    if os.path.exists("filmes.json"):
        with open("filmes.json", "r") as f:
            return json.load(f)
    return []

# Função para salvar filmes no arquivo JSON
def salvar_filmes(filmes):
    with open("filmes.json", "w") as f:
        json.dump(filmes, f, indent=4)

# Função para adicionar um novo filme
def adicionar_filme():
    titulo = input("Título do filme: ")
    ano = input("Ano de lançamento: ")
    genero = input("Gênero: ")
    diretor = input("Diretor: ")

    novo_filme = {
        "titulo": titulo,
        "ano": ano,
        "genero": genero,
        "diretor": diretor
    }

    filmes = carregar_filmes()
    filmes.append(novo_filme)
    salvar_filmes(filmes)
    print(f"\nFilme '{titulo}' adicionado com sucesso!\n")

# Função para listar todos os filmes
def listar_filmes():
    filmes = carregar_filmes()
    if filmes:
        print("\nCatálogo de Filmes:\n")
        for i, filme in enumerate(filmes, start=1):
            print(f"{i}. {filme['titulo']} ({filme['ano']}) - {filme['genero']} - Dirigido por {filme['diretor']}")
    else:
        print("\nNenhum filme cadastrado.\n")

# Função para remover um filme
def remover_filme():
    listar_filmes()
    filmes = carregar_filmes()
    index = int(input("\nNúmero do filme a remover: ")) - 1

    if 0 <= index < len(filmes):
        filme_removido = filmes.pop(index)
        salvar_filmes(filmes)
        print(f"\nFilme '{filme_removido['titulo']}' removido com sucesso!\n")
    else:
        print("\nOpção inválida.\n")

# Função principal para exibir o menu
def menu():
    while True:
        print("\n--- Catálogo de Filmes ---")
        print("1. Adicionar Filme")
        print("2. Listar Filmes")
        print("3. Remover Filme")
        print("4. Sair")
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            adicionar_filme()
        elif opcao == "2":
            listar_filmes()
        elif opcao == "3":
            remover_filme()
        elif opcao == "4":
            print("Saindo do catálogo de filmes...")
            break
        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    menu()
