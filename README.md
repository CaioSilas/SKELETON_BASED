# SKELETON_BASED_ACTION_RECOGNTION_PARA_RECONHECIMENTO_DE_LINGUAGEM_DE_SINAIS
Este repositório contém a implementação de um sistema de reconhecimento de sinais em Língua Brasileira de Sinais (LIBRAS) utilizando uma abordagem baseada em análise de dados de esqueleto.


O trabalho foi feito em conjunto com os alunos:
Beatriz Helena de Mello Orlandi de Deus,Julia Carlos Gonzaga,Josué Villa Real

O projeto propõe o uso de informações tridimensionais da base LibrasUFOP, extraídas por sensores e algoritmos de estimativa de pose, para capturar robustamente os gestos.
Principais características do projeto:


• Utilização de dados de esqueleto: O sistema foca exclusivamente em dados de esqueleto, o que reduz a complexidade computacional em comparação com abordagens multimodais.

• Arquitetura Transformer com Multi-Head Attention: A arquitetura central do sistema é um Transformer com mecanismo de Multi-Head Attention, que permite o processamento paralelo e a captura de relações temporais de longo alcance nos dados de esquelético. Este mecanismo aprende a ponderar a importância de diferentes partes da sequência de dados de esqueleto, identificando quais articulações e momentos são mais relevantes para o reconhecimento do sinal [our conversation history].

• Pré-processamento robusto: O projeto inclui etapas de filtragem e padronização dos dados de esqueleto, além da extração de derivadas temporais (velocidade e aceleração) para enriquecer a representação dos movimentos.

• Embeddings posicionais: A ordem temporal dos frames é preservada através da adição de embeddings posicionais à entrada do Transformer.

• Avaliação rigorosa: A metodologia emprega validação cruzada K-Fold para uma avaliação robusta da generalização do modelo. As métricas de avaliação incluem acurácia, precisão, revocação e F1-score.

• Resultados promissores: Os experimentos demonstraram uma alta acurácia no reconhecimento dos sinais, evidenciando a eficácia da abordagem Transformer para esta tarefa. A inclusão de derivadas temporais contribuiu para uma discriminação mais precisa entre gestos sutis.

• Simplicidade e eficiência: Ao focar em dados de esqueleto e utilizar a arquitetura Transformer, busca-se um sistema eficiente e de baixo custo computacional.
Este projeto visa aprimorar a comunicação e promover a inclusão social da comunidade surda através do desenvolvimento de tecnologias de reconhecimento automático da Língua Brasileira de Sinais.

Para trabalhos futuros, são consideradas a fusão multimodal com dados RGB e de profundidade, e a exploração de estratégias de aprendizado semi-supervisionado para reduzir a dependência de grandes volumes de dados anotados.