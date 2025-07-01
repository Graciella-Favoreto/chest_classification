# Classificação de Radiografias de Tórax com ResNet-50

Este projeto explora a classificação de imagens de radiografia de tórax em quatro classes distintas utilizando a arquitetura de rede neural convolucional ResNet-50. Foram implementadas e avaliadas duas abordagens de pré-processamento de imagem: uma utilizando as imagens completas e outra utilizando imagens segmentadas para isolar as regiões de interesse (pulmões).

## 📊 Visão Geral do Projeto

O objetivo principal é comparar a performance de um modelo de classificação treinado com imagens de raio-x padrão versus um treinado com imagens que tiveram os pulmões segmentados previamente, buscando identificar se o foco na região de interesse (ROI) melhora a precisão da classificação.

O projeto inclui:
* Dois notebooks de treinamento (`.ipynb`), um para cada abordagem.
* O uso da técnica de *transfer learning* com a rede ResNet-50 pré-treinada no dataset ImageNet.
* Otimização de hiperparâmetros (taxa de aprendizado, otimizador e tamanho do batch) utilizando a biblioteca Optuna.
* Avaliação detalhada dos modelos com matriz de confusão e relatório de classificação.

## 🗂️ Dataset

O projeto utiliza o dataset público **COVID-19 Radiography Dataset**. Este dataset contém imagens de radiografias de tórax divididas nas seguintes quatro classes:
* COVID
* Normal
* Opacidade Pulmonar (Lung Opacity)
* Pneumonia Viral

O dataset original também fornece máscaras de segmentação para cada imagem, que foram utilizadas na segunda abordagem do projeto.

## ⚙️ Metodologia

Foram treinados dois modelos ResNet-50, cada um com uma estratégia de dados diferente:

1.  **Modelo 1 - Imagens Completas (`ResNet_only_covid_dataset.ipynb`):** O modelo foi treinado diretamente com as imagens de radiografia completas, após o redimensionamento e a normalização padrão.

2.  **Modelo 2 - Imagens Segmentadas (ROIs) (`ResNet_only_covid_dataset_ROIs.ipynb`):** Antes do treinamento, as imagens passaram por um pré-processamento onde as máscaras foram aplicadas para remover ruídos e focar apenas na região dos pulmões (ROI).

Para ambos os modelos, o dataset foi dividido em conjuntos de treino (70%), validação (15%) e teste (15%).

## 📈 Resultados

Ambos os modelos alcançaram alta performance, demonstrando a eficácia da arquitetura ResNet-50 para esta tarefa. Abaixo estão os resultados detalhados para cada abordagem no conjunto de teste.

### Modelo 1: Imagens Completas

* **Acurácia no conjunto de teste: 94.24%**

**Relatório de Classificação:**

| Classe              | Precisão | Recall | F1-Score |
| :------------------ | :------- | :----- | :------- |
| COVID               | 0.97     | 0.97   | 0.97     |
| Opacidade Pulmonar  | 0.96     | 0.87   | 0.91     |
| Normal              | 0.92     | 0.98   | 0.95     |
| Pneumonia Viral     | 0.98     | 0.93   | 0.95     |

### Modelo 2: Imagens Segmentadas (ROIs)

* **Acurácia no conjunto de teste: 94.36%**

**Relatório de Classificação:**

| Classe              | Precisão | Recall | F1-Score |
| :------------------ | :------- | :----- | :------- |
| COVID               | 0.99     | 0.94   | 0.96     |
| Opacidade Pulmonar  | 0.95     | 0.88   | 0.92     |
| Normal              | 0.92     | 0.98   | 0.95     |
| Pneumonia Viral     | 0.96     | 0.97   | 0.97     |

### Conclusão dos Resultados

Ambos os modelos apresentaram resultados excelentes e muito próximos. O modelo treinado com **imagens segmentadas obteve uma acurácia ligeiramente superior**, sugerindo que focar na região de interesse pode trazer um pequeno benefício para a performance da classificação.
