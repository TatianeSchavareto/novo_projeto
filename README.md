#Trabalho de estrutura de dados
#inicio do codigo
class Nodo:
    def __init__(self, numero, cor):
        self.numero = numero
        self.cor = cor
        self.prox = None


class ListaEncadeada:#fila de chamada do programa
    def __init__(self):
        self.head = None

  def inserirSemPrioridade(self, nodo):
        if not self.head:
            self.head = nodo
        else:
            atual = self.head
            while atual.prox:
                atual = atual.prox
            atual.prox = nodo

  def inserirComPrioridade(self, nodo):
        if not self.head:
            self.head = nodo
        elif self.head.cor == "V":
            nodo.prox = self.head
            self.head = nodo
        else:
            atual = self.head
            while atual.prox and atual.prox.cor == "A":
                atual = atual.prox
            nodo.prox = atual.prox
            atual.prox = nodo

  def inserir(self, cor, numero): #prioridade da fila, A urgencia V da para aguardar
        nodo = Nodo(numero, cor)
        if not self.head:
            self.head = nodo
        elif cor == "V":
            self.inserirSemPrioridade(nodo)
        elif cor == "A":
            self.inserirComPrioridade(nodo)

  def imprimirListaEspera(self):#mostrar a lista de pasciente
        atual = self.head
        while atual:
            print(f"Cartão {atual.cor}: {atual.numero}")
            atual = atual.prox

  def atenderPaciente(self):#atendimento ao cliente
        if not self.head:
            print("Lista de espera vazia.")
        else:
            paciente = self.head
            self.head = self.head.prox
            print(f"Atendendo paciente com Cartão {paciente.cor}: {paciente.numero}")


def main():
    lista_espera = ListaEncadeada()
#menu incial do programa
    while True:
        print("\n=== MENU PRINCIPAL ===")
        print("1 - Adicionar paciente à fila")
        print("2 - Mostrar pacientes na fila")
        print("3 - Chamar próximo paciente")
        print("4 - Sair")

  opcao = input("Escolha uma opção: ")

#inserir a opção desejada
        if opcao == "1":
            cor = input("Informe a cor do cartão (A para amarelo, V para verde): ")
            numero = int(input("Informe o número do cartão: "))
            lista_espera.inserir(cor, numero)

  elif opcao == "2":
            print("\n=== PACIENTES NA FILA ===")
            lista_espera.imprimirListaEspera()

  elif opcao == "3":
            lista_espera.atenderPaciente()

  elif opcao == "4":
            print("Encerrando o programa...")
            break

  else:
           print("Opção inválida. Tente novamente.")


if __name__ == "__main__":
    main()



