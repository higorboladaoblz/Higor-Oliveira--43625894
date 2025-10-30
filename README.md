class Funcionario:
    def __init__(self, nome, cargo, salario):
        self.nome = nome
        self.cargo = cargo
        self.salario = salario
    
    def __str__(self):
        return f"Nome: {self.nome}, Cargo: {self.cargo}, Salário: R$ {self.salario:.2f}"


class GerenciadorFuncionarios:
    def __init__(self):
        self.funcionarios = []
    
    def adicionar_funcionario(self, nome, cargo, salario):
        self.funcionarios.append(Funcionario(nome, cargo, salario))
        print(f"✓ Funcionário {nome} adicionado com sucesso!")
    
    def listar_funcionarios(self):
        if not self.funcionarios:
            print("Nenhum funcionário cadastrado.")
            return
        print("\n" + "="*60)
        print("LISTA DE FUNCIONÁRIOS")
        print("="*60)
        for i, func in enumerate(self.funcionarios, 1):
            print(f"{i}. {func}")
        print("="*60 + "\n")
    
    def buscar_por_nome(self, nome):
        resultados = [f for f in self.funcionarios if nome.lower() in f.nome.lower()]
        if not resultados:
            print(f"Nenhum funcionário encontrado com o nome '{nome}'.")
            return
        print(f"\nResultados da busca por '{nome}':")
        print("-"*60)
        for func in resultados:
            print(func)
        print("-"*60 + "\n")
    
    def calcular_media_salarial(self):
        if not self.funcionarios:
            print("Nenhum funcionário cadastrado para calcular média.")
            return 0
        total = sum(f.salario for f in self.funcionarios)
        media = total / len(self.funcionarios)
        print(f"\nMédia Salarial: R$ {media:.2f}")
        print(f"Total de funcionários: {len(self.funcionarios)}")
        print(f"Folha de pagamento total: R$ {total:.2f}\n")
        return media


def menu():
    print("\n" + "="*60)
    print("SISTEMA DE GERENCIAMENTO DE FUNCIONÁRIOS")
    print("="*60)
    print("1. Adicionar funcionário")
    print("2. Listar funcionários")
    print("3. Buscar funcionário por nome")
    print("4. Calcular média salarial")
    print("5. Sair")
    print("="*60)


def main():
    g = GerenciadorFuncionarios()
    while True:
        menu()
        op = input("Escolha uma opção: ").strip()
        if op == "1":
            nome = input("\nNome: ").strip()
            cargo = input("Cargo: ").strip()
            try:
                salario = float(input("Salário: R$ ").strip())
                g.adicionar_funcionario(nome, cargo, salario)
            except ValueError:
                print("✗ Erro: Salário inválido.")
        elif op == "2":
            g.listar_funcionarios()
        elif op == "3":
            g.buscar_por_nome(input("\nNome para buscar: ").strip())
        elif op == "4":
            g.calcular_media_salarial()
        elif op == "5":
            print("\nEncerrando... Até logo!")
            break
        else:
            print("\n✗ Opção inválida!")

if __name__ == "__main__":
    main()
