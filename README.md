# Reconhecimento de Sinais em LIBRAS com Transformer sobre Esqueletos

Sistema de reconhecimento de sinais isolados da **Língua Brasileira de Sinais (LIBRAS)** usando apenas dados de esqueleto 3D e uma arquitetura **Transformer com Multi-Head Attention**.

**Resultado:** **84,1% de acurácia média (± 1,2)** em **29 sinais**, com validação cruzada 5-fold.

Trabalho feito em equipe com Beatriz Helena de Mello Orlandi de Deus, Julia Carlos Gonzaga e Josué Villa Real. Artigo completo em [`Artigo/`](Artigo/).

## Por que esqueletos?

Em vez de processar vídeo RGB, o modelo usa só as coordenadas (x, y, z) de **25 articulações** do corpo em cada frame. A entrada fica muito menor, o custo computacional cai e o modelo fica menos sensível a fundo, roupa e iluminação.

## Dados

- Base **LibrasUFOP**, versão com esqueletos (incluída em [`Base de Dados/`](Base%20de%20Dados/))
- Cerca de **1.600 amostras** segmentadas a partir de arquivos de anotação (frame inicial, frame final e rótulo)
- **29 classes** de sinais

## Pipeline

1. **Leitura e segmentação:** os arquivos de anotação definem o intervalo de frames de cada sinal.
2. **Normalização:** coordenadas centralizadas em uma articulação de referência e correção de frames com articulações faltando.
3. **Padding:** sequências ajustadas para 100 frames, com máscara para ignorar o preenchimento.
4. **Engenharia de atributos:** concatenação de **velocidade e aceleração** (derivadas temporais) às posições, o que ajuda a separar gestos parecidos.
5. **Modelo:**
   - embedding posicional para preservar a ordem dos frames
   - Multi-Head Attention (4 cabeças) com conexão residual e LayerNorm
   - camadas densas com regularização L2, Dropout e BatchNorm
   - Global Average Pooling no tempo e saída softmax
6. **Treino:** Adam, EarlyStopping e ReduceLROnPlateau.
7. **Avaliação:** K-Fold (k = 5) com acurácia, precisão, revocação e F1 (macro), além de matriz de confusão.

## Resultados

| Fold | Acurácia |
|---|---|
| 1 | 86% |
| 2 | 83% |
| 3 | 82% |
| 4 | 84% |
| 5 | 85% |
| **Média** | **84,1% ± 1,2** |

## Limitações e próximos passos

- **A divisão dos folds é por amostra, não por sinalizante.** A mesma pessoa pode aparecer no treino e no teste, então o resultado tende a ser otimista para pessoas novas. O próximo experimento é avaliar com *leave-one-signer-out*.
- Fusão com dados RGB e de profundidade
- Aprendizado semissupervisionado para reduzir a dependência de dados anotados

## Como executar

```bash
pip install tensorflow scikit-learn numpy matplotlib seaborn
```

1. Extraia `Base de Dados/LibrasUfop-skeleton.rar`.
2. Abra `Codigo/transformer.ipynb` e ajuste o caminho da base na primeira célula.
3. Execute as células em ordem.

## Tecnologias

Python · TensorFlow / Keras · scikit-learn · NumPy · Matplotlib · Seaborn
