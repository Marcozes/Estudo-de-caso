Portífolio-Computational Logic Using Python
eventos = {
    "Tech Week": {
        "descricao": "Palestras e workshops sobre inovação e segurança digital",
        "data": "10 a 13 de agosto",
        "max_participantes": 100,
        "inscritos": ["Marco", "Maria"]
    },
    "Feirão de Profissões": {
        "descricao": "Estandes de empresas e universidades parceiras",
        "data": "20 a 23 de agosto",
        "max_participantes": 100,
        "inscritos": ["Marco", "Maria"]
    }
}

def menu_principal():
    print("Sistema de Eventos UNIFECAF - Bem-vindo!")
    print("Deseja acessar como:")
    print("1 = Coordenador")
    print("2 = Aluno")
    print("3 = Sair")
    opcao = input("Selecione uma opção: ")

    if opcao == "1":
        menu_coordenador()
    elif opcao == "2":
        menu_aluno()
    elif opcao == "3":
        print("Saindo do sistema. Até logo!")
    else:
        print("Opção inválida. Tente novamente.")
        menu_principal()

def menu_coordenador():
    print("\nMenu do Coordenador")
    print("1 = Cadastrar Evento")
    print("2 = Atualizar Evento")
    print("3 = Excluir Evento")
    print("4 = Voltar ao Menu Principal")
    opcao = input("Selecione uma opção: ")

    if opcao == "1":
        cadastrar_evento()
    elif opcao == "2":
        atualizar_evento()
    elif opcao == "3":
        excluir_evento()
    elif opcao == "4":
        menu_principal()
    else:
        print("Opção inválida. Tente novamente.")
        menu_coordenador()

def menu_aluno():
    print("\nMenu do Aluno")
    print("1 = Visualizar Eventos Disponíveis")
    print("2 = Inscrever-se em Evento")
    print("3 = Lista de Alunos por Evento")
    print("4 = Voltar ao Menu Principal")
    opcao = input("Selecione uma opção: ")

    if opcao == "1":
        visualizar_eventos()
    elif opcao == "2":
        inscrever_evento()
    elif opcao == "3":
        listar_alunos_por_evento()
    elif opcao == "4":
        menu_principal()
    else:
        print("Opção inválida. Tente novamente.")
        menu_aluno()

def cadastrar_evento():
    nome_evento = input("\nDigite o nome do evento: ")
    descricao = input("Digite a descrição do evento: ")
    data = input("Digite a data do evento: ")
    max_participantes = int(input("Defina o número máximo de participantes: "))
    eventos[nome_evento] = {
        "descricao": descricao,
        "data": data,
        "max_participantes": max_participantes,
        "inscritos": []
    }
    print(f"Evento '{nome_evento}' cadastrado com sucesso!")
    input("Aperte Enter para continuar...")
    menu_coordenador()

def atualizar_evento():
    nome_evento = input("\nDigite o nome do evento a atualizar: ")
    if nome_evento in eventos:
        nova_data = input("Digite a nova data do evento: ")
        nova_max_participantes = int(input("Digite a nova quantidade máxima de participantes: "))
        eventos[nome_evento]["data"] = nova_data
        eventos[nome_evento]["max_participantes"] = nova_max_participantes
        print(f"Evento '{nome_evento}' atualizado com sucesso!")
    else:
        print("Evento não encontrado.")
    input("Aperte Enter para continuar...")
    menu_coordenador()

def excluir_evento():
    nome_evento = input("\nDigite o nome do evento a excluir: ")
    if nome_evento in eventos:
        confirmacao = input(f"Esta ação é irreversível. Deseja realmente excluir o evento '{nome_evento}'? (s/n): ")
        if confirmacao.lower() == "s":
            del eventos[nome_evento]
            print(f"Evento '{nome_evento}' excluído com sucesso!")
        else:
            print("Exclusão cancelada.")
    else:
        print("Evento não encontrado.")
    input("Aperte Enter para continuar...")
    menu_coordenador()

def visualizar_eventos():
    print("\nEventos disponíveis para inscrição:")
    for nome, detalhes in eventos.items():
        vagas = detalhes["max_participantes"] - len(detalhes["inscritos"])
        print(f"{nome}: {detalhes['descricao']} | {detalhes['data']} | Vagas: {len(detalhes['inscritos'])}/{detalhes['max_participantes']}")
    input("Aperte Enter para continuar...")
    menu_aluno()

def inscrever_evento():
    nome_evento = input("\nDigite o nome do evento que deseja se inscrever: ")
    if nome_evento in eventos:
        evento = eventos[nome_evento]
        if len(evento["inscritos"]) >= evento["max_participantes"]:
            print("Vagas esgotadas para este evento. Selecione uma opção ainda disponível.")
        elif input("Digite seu nome: ") in evento["inscritos"]:
            print("Você já está inscrito neste evento.")
        else:
            nome_aluno = input("Digite seu nome: ")
            evento["inscritos"].append(nome_aluno)
            print(f"Inscrição realizada com sucesso no evento '{nome_evento}'!")
    else:
        print("Evento não encontrado.")
    input("Aperte Enter para continuar...")
    menu_aluno()

def listar_alunos_por_evento():
    nome_evento = input("\nDigite o nome do evento para listar os alunos: ")
    if nome_evento in eventos:
        print(f"Alunos inscritos no evento '{nome_evento}':")
        for aluno in eventos[nome_evento]["inscritos"]:
            print(f"- {aluno}")
    else:
        print("Evento não encontrado.")
    input("Aperte Enter para continuar...")
    menu_aluno()

# Início do programa
menu_principal()
