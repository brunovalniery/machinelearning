# Comparativo de CNNs para Classificação no CIFAR-10

Este documento fornece informações sobre os modelos de redes neurais convolucionais (CNNs) e foi desenvolvido como parte do projeto final da disciplina de Machine Learning.

## 1. Detalhes do modelo

- **Autor:** Bruno Valniery
- **Data:** Julho de 2025
- **Versão do Modelo:** 1.0
- **Tipo:** Redes Neurais Convolucionais (CNN) para classificação de imagens.
- **Informações de Contato:** bruno.sousa.018@ufrn.edu.br

---

## 2. Intenção de uso

- **Uso principal:** O objetivo primário destes modelos é acadêmico. Foram desenvolvidos para aprender, implementar, comparar e analisar diferentes arquiteturas de CNNs, aplicando técnicas de otimização e avaliação.
- **Usuários-alvo:** Estudantes, pesquisadores e entusiastas de Machine Learning interessados em visão computacional.
- **Usos fora do escopo:** Esses modelos não devem ser utilizados em sistemas de produção ou aplicações críticas no mundo real. Sua performance é avaliada apenas no contexto do dataset CIFAR-10 e não garante generalização para outros tipos de imagem ou cenários.

---

## 3. Dados de treinamento e avaliação

### 3.1. Dataset
- **Fonte:** **CIFAR-10**.
- **Descrição:** O dataset consiste em 60.000 imagens coloridas de 32x32 pixels, divididas em 10 classes mutuamente exclusivas (avião, carro, pássaro, gato, veado, cachorro, sapo, cavalo, navio, caminhão).
- **Divisão:**
  - **Treinamento:** 40.000 imagens (80% do conjunto de treino original).
  - **Validação:** 10.000 imagens (20% do conjunto de treino original).
  - **Teste:** 10.000 imagens (conjunto de teste original).

### 3.2. Pré-processamento
- As imagens foram normalizadas para terem valores de pixel no intervalo `[-1, 1]`, com média `0.5` e desvio padrão `0.5` para cada canal de cor (RGB). Esta transformação ajuda a estabilizar e acelerar o treinamento.

---

## 4. Procedimento de treinamento

- **Framework:** PyTorch
- **Otimizador:** Adam
- **Função de Perda:** `CrossEntropyLoss` (adequada para classificação multiclasse).
- **Taxa de Aprendizagem (Learning Rate):** A taxa inicial de `1e-3` foi escolhida com base na análise da técnica **FindingLR**, que identificou a região de maior declínio da perda.
- **Épocas:** Cada modelo foi treinado por `10` épocas.
- **Hardware:** Treinado em ambiente Google Colab com GPU (NVIDIA T4 ou similar).

---

## 5. Análise quantitativa e resultados

A performance de quatro arquiteturas distintas foi comparada.

### **Comparação das Curvas de Perda na Validação**

O gráfico abaixo ilustra a convergência de cada modelo. O "Meu Modelo", com *Batch Normalization* e *Dropout*, demonstrou a menor perda de validação e a maior estabilidade, indicando melhor generalização.

![Comparação das Curvas de Perda](./assets/compperdavalid.png)

---

### **Modelo 1: Modelo Base**

- **Arquitetura:** CNN simples com 2 camadas convolucionais.
- **Análise:** Serviu como um baseline. A matriz de confusão mostra dificuldades significativas em distinguir classes similares como `cat` vs. `dog`.

![Matriz de Confusão do Modelo Base](./assets/modelobase.png)

---

### **Modelo 2: Modelo Base + Variação de `n_feature`**

- **Arquitetura:** Idêntica ao Modelo Base, mas com o dobro de filtros na primeira camada (64 em vez de 32).
- **Análise:** O aumento na capacidade do modelo (mais features) resultou em uma melhora notável na acurácia, confirmando que o Modelo Base era limitado.

![Matriz de Confusão com n_feature=64](./assets/nfeatures.png)

---

### **Modelo 3: Modelo com Blocos**

- **Arquitetura:** CNN mais profunda com 3 blocos convolucionais modulares.
- **Análise:** A profundidade adicional permitiu que o modelo aprendesse features mais complexas e hierárquicas, resultando em um salto de performance.

![Matriz de Confusão do Modelo com Blocos](./assets/modeloblocos.png)

---

### **Modelo 4: Meu Modelo (proposta otimizada)**

- **Arquitetura:** CNN profunda com 3 camadas convolucionais, cada uma seguida por *Batch Normalization*, e uma camada de *Dropout* antes da classificação final.
- **Análise:** Este modelo alcançou o melhor desempenho. *Batch Normalization* estabilizou o treinamento, permitindo uma convergência mais rápida, enquanto o *Dropout* ajudou a regularizar o modelo, melhorando sua capacidade de generalização e reduzindo o overfitting.

![Matriz de Confusão do Seu Modelo](./assets/meumodelo.png)

---

## 6. Análise qualitativa com Hooks

A investigação das saídas das camadas intermediárias do **"Meu Modelo"** revelou que as camadas iniciais aprenderam a detectar características simples (bordas, cores), enquanto as camadas mais profundas aprenderam a identificar texturas e partes de objetos mais complexas.

![Visualização dos Hooks da Camada Conv3](./assets/saida1.png)

![Visualização dos Hooks da Camada Conv3](./assets/saida2.png)

---

## 7. Limitações e considerações

- **Viés do Dataset:** O CIFAR-10, embora seja um padrão para benchmarks, não representa a diversidade de imagens do mundo real. Os modelos treinados neste dataset podem não performar bem em imagens com diferentes iluminações, ângulos ou contextos culturais.
- **Generalização:** A performance é garantida apenas para imagens muito similares às do CIFAR-10.
- **Interpretabilidade:** Embora os *hooks* forneçam algum insight, os modelos de deep learning ainda operam em grande parte como "caixas-pretas", e suas decisões podem ser difíceis de justificar completamente.

---

## 8. Como utilizar

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/brunovalniery/machinelearning.git
    ```
2.  **Abra no Google Colab:**
    - Vá para [colab.research.google.com](https://colab.research.google.com).
    - Clique em `File > Upload notebook` e selecione o arquivo do projeto.
3.  **Execute as células:**
    - Ative o ambiente com GPU (`Runtime > Change runtime type > GPU`).
    - Execute as células em ordem para reproduzir os resultados.

