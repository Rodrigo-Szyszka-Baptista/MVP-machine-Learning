# MVP-machine-Learning
Projeto de Machine Learning cursdo de pós graduação da PUC Rio

1. Introdução
O spam em mensagens de texto (SMS) é um problema recorrente que afeta usuários e organizações, causando desde inconvenientes até riscos financeiros e de segurança. A identificação automática dessas mensagens é fundamental para evitar fraudes, golpes e sobrecarga de sistemas de comunicação.
Este projeto tem como objetivo desenvolver um modelo de aprendizado de máquina capaz de classificar mensagens SMS em duas categorias:
  •	ham (0): mensagens legítimas
  •	spam (1): mensagens não solicitadas ou fraudulentas
O trabalho foi conduzido de acordo com as boas práticas de ciência de dados, incluindo análise exploratória, preparação de dados, modelagem, ajuste de hiperparâmetros e avaliação de resultados.

2. Definição do Problema
Descrição: Classificar automaticamente mensagens SMS em ham ou spam, utilizando aprendizado supervisionado.
Premissas:
  •	Mensagens de spam apresentam padrões linguísticos recorrentes (palavras como “free”, “win”, “congratulations”, links suspeitos).
  •	Modelos supervisionados podem aprender a distinguir spam de ham a partir de exemplos rotulados.
Restrições:
  •	Dataset limitado a mensagens de texto.
  •	Não há metadados adicionais (horário, remetente, etc.).
  •	Deseja-se priorizar o equilíbrio entre precisão e recall, evitando tanto falsos positivos quanto falsos negativos.
Dataset:
  •	Origem: repositório público com 5.574 mensagens rotuladas.
  •	Estrutura:
o	label: classe (ham ou spam).
o	text: conteúdo textual da mensagem.


3. Preparação dos Dados
  1.	Limpeza: não foram identificados valores ausentes relevantes.
  2.	Codificação dos rótulos: transformação de ham/spam em valores binários (0/1).
  3.	Representação do texto: utilização de TF-IDF Vectorizer, técnica que transforma textos em vetores numéricos considerando a relevância das palavras.
  4.	Divisão dos dados:
      o	70% para treino
      o	30% para teste
      o	Validação cruzada (k-fold) para reduzir viés da divisão aleatória.

4. Modelagem
Foram avaliados quatro algoritmos clássicos de classificação:
  •	Naive Bayes: modelo probabilístico simples, frequentemente utilizado como baseline em problemas de NLP.
  •	Regressão Logística: modelo linear com boa interpretabilidade.
  •	Random Forest: ensemble de árvores de decisão, capaz de capturar interações não lineares.
  •	SVM Linear (Support Vector Machine): adequado para dados de alta dimensionalidade, como representações textuais.
Ajuste de Hiperparâmetros:
  •	Foi aplicado GridSearchCV para afinar o modelo SVM, que apresentou melhor desempenho inicial.
  •	Parâmetros ajustados: penalização C, métodos de calibração de probabilidades.

5. Avaliação
Métricas Utilizadas
  •	Accuracy: proporção de acertos totais.
  •	Precision: proporção de mensagens classificadas como spam que realmente eram spam.
  •	Recall: proporção de mensagens de spam corretamente identificadas.
  •	F1-score: média harmônica entre precisão e recall.
  •	AUC (ROC Curve): capacidade de separação entre classes em diferentes limiares.
Resultados na Validação
Modelo	Accuracy	Precision	Recall	F1	AUC
Linear SVM	0.986	0.972	0.919	0.945	0.992
Random Forest	0.971	1.000	0.785	0.880	0.989
Naive Bayes	0.969	1.000	0.768	0.867	0.989
Regressão Logística	0.963	1.000	0.723	0.839	0.990
					
O modelo Linear SVM apresentou o melhor equilíbrio entre precisão e recall, além do maior F1 e AUC.

6. Modelo Final
Após ajuste de hiperparâmetros, o modelo final selecionado foi o SVM Linear calibrado.
Resultados no Conjunto de Teste
  •	Accuracy: 0.985
  •	Precision: 0.94
  •	Recall: 0.92
  •	F1-score: 0.95
  •	AUC: 0.988
Matriz de Confusão (Teste):
  •	Verdadeiros Ham: 718
  •	Falsos Spam: 6
  •	Verdadeiros Spam: 103
  •	Falsos Ham: 9
O modelo demonstrou boa capacidade de generalização, sem sinais de overfitting.

7. Conclusão
O modelo SVM Linear mostrou-se a melhor solução para o problema de classificação de mensagens SMS em ham e spam, alcançando métricas elevadas em precisão, recall e AUC.
Limitações:
  •	Dataset restrito a mensagens em inglês e relativamente pequeno.
  •	Não inclui fatores contextuais adicionais, como comportamento do remetente ou histórico de mensagens.
Possíveis melhorias:
  •	Ampliar o dataset com exemplos atuais e multilíngues.
•	Avaliar modelos de Deep Learning (redes neurais recorrentes, transformers).
•	Considerar técnicas de ensemble para combinar previsões de diferentes modelos.
