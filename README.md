# Summit-UMC-2025-Group42-
Summit UMC 2025 Group42 - SVM Heart Disease Dataset, KFold(k=10) x Leave-P-Out(p=2)


##Documentação do Projeto de Classificação de Doença Cardíaca

Este projeto utiliza o algoritmo de Machine Learning Support Vector Machine (SVM) para classificar a presença de doença cardíaca com base em um conjunto de dados do UCI (Universidade da Califórnia em Irvine). O notebook Colab executa duas abordagens de validação cruzada para avaliar o modelo: K-Fold e Leave-P-Out (p=2).

##Estrutura do Projeto:

O projeto é dividido em duas seções principais, cada uma explorando uma técnica de validação cruzada diferente para garantir a robustez e a confiabilidade dos resultados do modelo. Ambas as seções seguem um fluxo de trabalho similar:

 * Importação de Bibliotecas: Carrega as bibliotecas necessárias, como Pandas para manipulação de dados, Scikit-learn para machine learning, e Matplotlib/Seaborn para visualização.
 * Carregamento e Pré-processamento de Dados: Lê o arquivo heart_disease.csv, converte todos os valores para numéricos, tratando dados faltantes com NaN (Not a Number), e transforma a variável alvo (num) em um formato binário (0 = sem doença, 1 = com doença).
 * Divisão dos Dados: Separa o conjunto de dados em variáveis independentes (X) e a variável alvo (y). Em seguida, divide esses dados em conjuntos de treino (80%) e teste (20%) usando train_test_split, com stratify=y para manter a proporção de classes em ambos os conjuntos. O random_state=42 garante a reprodutibilidade dos resultados.
 * Tratamento e Padronização: Utiliza SimpleImputer para substituir valores ausentes (NaN) pela média dos dados de treino. Em seguida, usa StandardScaler para padronizar as variáveis, garantindo que a média seja 0 e o desvio padrão seja 1. O fit é aplicado apenas aos dados de treino para evitar data leakage, ou seja, para que o modelo não "aprecenda" com informações do conjunto de teste antes da avaliação.
 * Treinamento e Otimização do Modelo: Utiliza GridSearchCV para encontrar a melhor combinação de hiperparâmetros para o modelo SVM. O param_grid especifica diferentes valores para os parâmetros kernel (linear e RBF), C (parâmetro de regularização) e gamma (parâmetro do kernel RBF).
Análise K-Fold (k=10)
Esta seção utiliza a validação cruzada K-Fold com 10 "folds". Isso significa que o conjunto de dados de treino é dividido em 10 subconjuntos, e o modelo é treinado e testado 10 vezes. A cada rodada, um subconjunto diferente é usado para teste, e o modelo é treinado nos 9 subconjuntos restantes.
Resultados Principais:
 * Melhores Parâmetros: {'C': 0.01, 'kernel': 'linear'}
 * Acurácia Média (Validação Cruzada): 0.852 ± 0.072
 * Acurácia no Conjunto de Teste: 0.770
 * Falsos Positivos: 5 (o modelo previu "doença" quando o paciente não a tinha)
 * Falsos Negativos: 9 (o modelo previu "sem doença" quando o paciente a tinha)
Análise Leave-P-Out (p=2)
Esta seção utiliza a validação cruzada Leave-P-Out, onde p=2. Isso significa que o modelo é treinado em todas as amostras, exceto duas, que são usadas para teste. Este processo é repetido para cada combinação possível de duas amostras. Embora seja computacionalmente mais intensivo, ele pode ser útil em conjuntos de dados menores.
Resultados Principais:
 * Melhores Parâmetros: {'C': 1, 'gamma': 0.001, 'kernel': 'rbf'}
 * Acurácia Média (Validação Cruzada): 0.853
 * Acurácia no Conjunto de Teste: 0.787
 * Falsos Positivos: 2 (o modelo previu "doença" quando o paciente não a tinha)
 * Falsos Negativos: 11 (o modelo previu "sem doença" quando o paciente a tinha)
Conclusão e Comparação das Abordagens
Ambas as abordagens de validação cruzada encontraram um modelo SVM com desempenho similar. A acurácia média de validação cruzada foi de 0.852 (K-Fold) e 0.853 (Leave-P-Out), mostrando que o modelo tem uma performance consistente.
No conjunto de teste, o modelo otimizado com Leave-P-Out (kernel RBF) obteve uma acurácia ligeiramente superior (0.787) em comparação com o modelo K-Fold (kernel linear) (0.770).
A matriz de confusão revela as diferenças mais significativas:
 * O modelo K-Fold teve mais falsos positivos (5), o que significa que mais pessoas saudáveis foram incorretamente diagnosticadas como doentes.
 * O modelo Leave-P-Out teve um número menor de falsos positivos (2) mas um número maior de falsos negativos (11), indicando que ele errou mais ao não identificar pacientes que realmente tinham a doença. Dependendo da aplicação, a escolha entre esses modelos dependeria do custo associado a cada tipo de erro.
