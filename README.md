def cadastro_dados():
  disciplina = input("Disciplina: ")

  notas = []

  primeira_nota = float(input("Digite a primeira nota do aluno: "))
  if primeira_nota < 0 or primeira_nota > 10:
    print("Nota inválida!")
    primeira_nota = float(input("Digite novamente: "))
  notas.append(primeira_nota)

  segunda_nota = float(input("Digite a segunda nota do aluno: "))
  if segunda_nota < 0 or segunda_nota > 10:
    print("Nota inválida!")
    segunda_nota = float(input("Digite novamente: "))
  notas.append(segunda_nota)

  total_faltas = int(input("Digite o número de faltas do aluno: "))
  if total_faltas < 0:
    print("Faltas inválidas!")
    total_faltas = int(input("Digite novamente: "))

  return disciplina, notas, total_faltas


def calcular_nota(notas):
  media = ((notas[0] * 7) + (notas[1] * 5)) / 12
  return media


def calcular_frequencia(media, faltas):
  if media >= 6 and faltas < 20:
    return "Aprovado"
  else:
    return "Reprovado"


def gerar_relatorio(escola, aluno, boletim):
  print(f"\n{escola}")
  print(" ---boletim--- \n")
  print(f"Aluno: {aluno}")

  for disciplina, dados in boletim.items():
    print(f"{disciplina}: {dados['resultado']}! média: {dados['media']:.2f}; faltas: {dados['faltas']}")


aluno = input("Nome do aluno: ")
escola = "Escola Pimpolho"
boletim = {}

proximo = 1

while proximo == 1:

  disciplina, notas, total_faltas = cadastro_dados()

  media = calcular_nota(notas)

  resultado = calcular_frequencia(media, total_faltas)

  if resultado == "Aprovado":
    print(f"Aprovado! média: {media:.2f}; faltas: {total_faltas}")
  else:
    print(f"Reprovado! média: {media:.2f}; faltas: {total_faltas}")

  boletim[disciplina] = {
    "resultado": resultado,
    "media": media,
    "faltas": total_faltas
  }

  continuar = input("Deseja cadastrar outra disciplina? (s/n): ")

  if continuar == "s":
    proximo = 1

  elif continuar == "n":
    proximo = 0

  else:
    print("Opção invalida!")
    continuar = input("Digite novamente (s/n): ")

    if continuar == "n":
      break


gerar_relatorio(escola, aluno, boletim)
