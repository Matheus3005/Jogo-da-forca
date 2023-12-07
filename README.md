# Jogo-da-forca
Um projeto de faculdade, programado em python. É um jogo básico da forca de times do Brasil.

import random





#variável para os times brasileiros

palavras= ["corinthians", "palmeiras", "santos", "são paulo", "flamengo", "fluminense", "vasco",

           "botafogo", "gremio", "internacional", "cuiaba", "atletico-mg", "atletico-pr",

           "cruzeiro", "coritiba", "fortaleza", "goias", "bragantino", "bahia", "america-mg"]





#função para escolher um time aleatório

def escolher_palavra():

    return random.choice(palavras)



#função para jogar

def jogar_forca():

    palavra=escolher_palavra()

    letra_erradas=""

    letra_certas=""

    tentativas=6



    while True:

        palavra_secreta=""

        for letra in palavra:

            if letra in letra_certas:

                palavra_secreta += letra

            else:

                palavra_secreta += "_"

            

        print("Palavra: " + palavra_secreta)

        print("Letras erradas: " + letra_erradas)

        print("Tentativas restantes: " + str(tentativas))



        if palavra_secreta == palavra:

            print("Você acertou! A palavra é: " + palavra)

            jogador = input("Digite seu nome: ")

            salvar_pontuacao(jogador, 10)

            break



        if tentativas == 0:

            print("Você perdeu!!! A palavra era: " + palavra)

            jogador = input("Digite seu nome: ")

            salvar_pontuacao(jogador, 0)

            break



        letra = input("Digite uma letra")



        if len(letra) != 1:

            print("Por favor, digite apenas uma letra!")

            continue



        if letra in palavra:

            letra_certas += letra

        else:

            letra_erradas += letra

            tentativas -= 1



#função para salvar as pontuações

def salvar_pontuacao(jogador, pontuacao):

        with open("pontuacoes.txt", "a") as arquivo:

            arquivo.write(jogador + ":" + str(pontuacao) + "\n")

        

        

#função para mostra as pontuações        

def mostrar_pontuacoes():

    try:

        with open("pontuacoes.txt", "r") as arquivo:

            pontuacoes = arquivo.readlines()

            print("Pontuações: ")

            for linha in pontuacoes:

                print(linha.strip())

        if pontuacoes:

            media = calcular_media(pontuacoes)

            print(f"Média das pontuações: {media:.2f}")

    except FileNotFoundError:

        print("Ainda não há pontuações registradas.")





#função para calcular a média

def calcular_media(pontuacoes):

    total_pontuacoes = 0

    total_jogadores = 0

    for linha in pontuacoes:

        jogador, pontuacao = linha.strip().split(":")

        total_pontuacoes += int(pontuacao)

        total_jogadores += 1

    if total_jogadores > 0:

        return total_pontuacoes / total_jogadores

    else:

        return 0

    



#menu do jogo

while True:

    print("-----------------------------------")

    print(" JOGO DA FORCA DOS TIMES DA SÉRIE A")

    print("-----------------------------------")

    print("---------- BEM-VINDO --------------")

    print("1- Jogar")

    print("2- Mostrar pontuação")

    print("3- Sair")

    opcao= input("Escolha uma opção: ")

    

    if opcao== "1":

        jogar_forca()

    elif opcao == "2":

        mostrar_pontuacoes()

    elif opcao == "3":

        break

    else:

        print("Opção inválida. Tente novamente.")
