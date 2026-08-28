# 🩺 Calculadora de Saúde e Bem-Estar

Projeto desenvolvido para a disciplina de **Garantia da Qualidade de Software (GQS)**, com o objetivo de identificar, corrigir e documentar inconsistências lógicas, erros de tipo e falhas no fluxo de execução de um sistema em Python.

---

## 📋 Descrição do Projeto

A **Calculadora de Saúde e Bem-Estar** é uma aplicação interativa via linha de comando (CLI) que permite aos usuários calcular e monitorar métricas essenciais de saúde e condicionamento físico:

1. **Índice de Massa Corporal (IMC):** Calcula o IMC a partir do peso e altura e exibe a respectiva classificação de acordo com os padrões da OMS.
2. **Recomendação Diária de Água:** Calcula a quantidade diária recomendada de ingestão de água (em litros) baseada no peso corporal (fórmula padrão de 35 ml/kg).
3. **Frequência Cardíaca Máxima (FCM):** Estima a frequência cardíaca máxima recomendada para treinos com base na idade (fórmula de Tanaka/Fox: `220 - idade`).

---

## 🐛 Relatório de Bugs Encontrados e Corrigidos

A tabela abaixo detalha as inconsistências identificadas no código original e as respectivas soluções aplicadas:

| # | Local do Bug (Função / Linhas) | Comportamento Incorreto Observado | Solução Aplicada |
|---|--------------------------------|-----------------------------------|------------------|
| **1** | `calcular_imc` (L3-L5 / L45) | **Divisão por Zero / Altura Nula:** Ao inserir altura `0` ou valor negativo, o programa lançava exceção `ZeroDivisionError` ou produzia IMC incoerente. | Adicionada validação para garantir que peso e altura sejam estritamente maiores que zero (`> 0`) antes do cálculo. |
| **2** | `calcular_imc` (L45-L46) | **Inconsistência de Unidade (cm vs m):** Caso o usuário digitasse a altura em centímetros (ex.: `175` em vez de `1.75`), o cálculo resultava em um IMC próximo de zero, classificando incorretamente como "Abaixo do peso". | Implementado ajuste/validação automática: se a altura inserida for maior que 3 (indicando centímetros), o valor é convertido dividindo-se por 100. |
| **3** | `calcular_agua_diaria` (L17-L19 / L51) | **Ausência de Validação de Peso Positivo:** O programa aceitava pesos negativos ou nulos, retornando metas diárias de água negativas (ex.: `-2.10 Litros`). | Adicionada verificação de valor positivo para o peso corporal antes de efetuar a operação matemática. |
| **4** | `calcular_frequencia_cardiaca_maxima` (L21-L23 / L56) | **Idade Inválida / FC Negativa:** Inserção de idades negativas ou superiores a 220 resultava em frequências cardíacas incoerentes ou negativas (ex.: idade 230 resultava em `-10 bpm`). | Incluída validação de faixa etária plausível (`0 < idade < 125`), alertando o usuário caso o valor seja inválido. |
| **5** | `menu` / `main` (L34, L40-L71) | **Tratamento Frágil de Entradas Não Numéricas:** A conversão direta `int(input())` na função `menu()` sem tratamento interno delegava o erro para o `try/except` global em `main`, reiniciando o loop abruptamente sem clareza para o usuário. | Modularizado o tratamento de exceções com loops de validação (`while True` com `try-except`) tanto no menu quanto na entrada de cada parâmetro específico. |

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- **Python 3.8+** instalado no ambiente ([Download Python](https://www.python.org/downloads/)).
- Git instalado (opcional, para clonagem).

### Passo a Passo

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/KdAndrade/gqs-calculadora-saude-py.git
   cd gqs-calculadora-saude-py
   ```

2. **Execute a aplicação:**
   ```bash
   python calculadora_saude.py
   ```
   *(ou `python3 calculadora_saude.py` dependendo do seu sistema operacional)*

3. **Interaja com o menu numérico:**
   - Digite `1` para calcular o IMC.
   - Digite `2` para calcular a recomendação de água.
   - Digite `3` para estimar a frequência cardíaca máxima.
   - Digite `4` para encerrar o programa.

---

## 🛠️ Tecnologias Utilizadas
- **Linguagem:** Python 3
- **Versionamento:** Git & GitHub
