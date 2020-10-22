# Jogo-da-Forca
# Jogo da forca com duas opções, escrever uma palavra, ou receber uma palavra aleatoria do banco de dados do programa

from random import randint

biblioteca = ['gabriel', 'cachorro', 'papagaio', 'paralelepipedo', 'guarda chuba', 'pato', 'aquecimento vocal',
              'vaso de flores', 'leite', 'gato', 'mordida', 'python', 'java', 'html', 'windows', 'linux', 'macos',
              'teclado', 'mouse', 'monitor', 'microfone']
digt_or_pre = int(input('Você deseja digitr a palavra ou quer que o programa selecione uma aleatoria?\n'
                        '[ 1 ]Para digitar e [ 2 ]Para palavra aleatoria : '))
# Palavra Chave.
if digt_or_pre == 1:
    palavra = str(input('Digite a Palavra chave: ')).upper()
elif digt_or_pre == 2:
    palavra = biblioteca[randint(0, len(biblioteca))]
palavra.upper()

# Banco de dados.
palavra_lista = []
contador_misto = 0
palavra_underline = {}
win = 0
quat_digitado = 0
letras_digitadas = ''
cont_erros = 6
letras_digitadas_2 = ''

if palavra.find(' '):
    win += palavra.count(' ')

# Criando uma lista da "palavra" em letras separadas.
for palavra_lista_print in palavra:
    palavra_lista.append(palavra[contador_misto])
    contador_misto += 1
contador_misto = 0

# Criando uma lista onde as letras da "palavra" vão entrar.
for underline in palavra:
    if palavra[contador_misto] != ' ':
        palavra_underline[contador_misto] = '_'
    else:
        palavra_underline[contador_misto] = '-'
    contador_misto += 1
contador_misto = 0

# Print Inf. Da palavra.
print('=' * 60)
print(f'A palavra tem: \033[44m{len(palavra)}\033[m letras.')

for underline_print in palavra_underline.values():
    print(f'\033[34m{underline_print}\033[m', end=' ')
print()
print('=' * 60)

contador_misto = 0

# Repetição
while True:

    if win >= len(palavra):
        print('\033[33m=' * 60)
        print('Parabéns, Você ganhou!!')
        print('=' * 60)
        print('\033[m')
        break


    if quat_digitado == 0:
        letra = str(input('Digite uma letra da Palavra: ')).upper()
        contador_misto = 0

    if len(letra) > 1:
        letra = letra[0]

    if letra in palavra:

        if letra not in letras_digitadas:
            quat_digitado = 0
            win += palavra.count(letra)

            # Adicionando "letra" á "palavra"
            for underline_valor in palavra_underline.values():
                if letra == palavra[contador_misto]:
                    palavra_underline[contador_misto] = letra

                else:
                    palavra_underline[contador_misto] = palavra_underline[contador_misto]
                contador_misto += 1

            letras_digitadas += letra
            print('=' * 60)
            for underline_print in palavra_underline.values():
                print(f'\033[34m{underline_print}\033[m', end=' ')
            print()
            print('=' * 60)

        elif letra in letras_digitadas:
            while True:
                letra = str(input(f'A letra "{letra}" já foi digitada.\n'
                                  f'Digite outra letra: ')).upper()
                quat_digitado = 1
                break

    elif letra not in palavra:

        while True:
            cont_erros -= 1
            if cont_erros == 0:
                print('\033[31m')
                print('=' * 60)
                print(f'Você perdeu!!A palavra era:\n'
                      f'\033[31m"{palavra}"\033[m')
                print('\033[31m=' * 60)
                print('\033[m')
                break

            letra = str(input(f'\033[31mVocê errou!A letra "{letra}" não estava na palavra,'
                              f'Você tem mais {cont_erros} tentativas.\n'
                              f'Digite outra letra: \033[m')).upper()

            quat_digitado = 1
            break

        if cont_erros == 0:
            break


