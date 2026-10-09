# Classificação de Famílias de Peixes com SVM

Projeto desenvolvido na disciplina de Inteligência Artificial, utilizando Python no Google Colab para prever a família de um peixe a partir de suas características numéricas.

## Dataset

O arquivo `FISHMORPH_Family_Dataset.csv` contém 8.342 registros, 10 características numéricas e a coluna `Family`, utilizada como alvo da classificação. A base possui 197 famílias de peixes.

As características utilizadas são: `MBl`, `BEl`, `VEp`, `REs`, `OGp`, `RMl`, `BLs`, `PFv`, `PFs` e `CPt`.

## Etapas do projeto

- Importação do dataset no Google Colab.
- Análise do tamanho da base, tipos das colunas e estatísticas descritivas.
- Verificação de valores nulos e registros duplicados.
- Contagem e gráfico da distribuição das famílias.
- Separação das características (`X`) e do alvo (`y`).
- Divisão de 80% dos registros para treino e 20% para teste.
- Padronização com `StandardScaler` e classificação com SVM (`SVC`) em um `Pipeline`.
- Busca de hiperparâmetros com `GridSearchCV` e validação cruzada em cinco partes.
- Cálculo da acurácia e visualização da matriz de confusão para as 15 famílias mais frequentes no conjunto separado para teste.

## Hiperparâmetros testados

| Hiperparâmetro | Valores |
| --- | --- |
| Kernel | `linear`, `poly`, `rbf`, `sigmoid` |
| C | `0.1`, `1`, `10`, `100` |
| Gamma | `0.001`, `0.01`, `0.1`, `1` |

São 64 combinações, avaliadas em cinco divisões. O parâmetro `gamma` não altera o kernel linear.

## Resultados registrados no notebook

| Item | Resultado |
| --- | --- |
| Modelo selecionado | SVM (`SVC`) com padronização |
| Kernel | `rbf` |
| C | `10` |
| Gamma | `0.1` |
| Acurácia média na validação cruzada | 61,92% |
| Acurácia exibida no subconjunto separado para teste | 81,97% |

**Atenção à avaliação:** o notebook executa `grid.fit(X, y)`, utilizando toda a base, inclusive os registros separados para teste. Portanto, os 81,97% não representam desempenho em dados inéditos. Para obter uma avaliação independente, é necessário treinar com `grid.fit(X_train, y_train)`, prever com `grid.best_estimator_.predict(X_test)` e recalcular os resultados.

## Observações sobre a versão atual

- Não foram encontrados valores nulos. Foi identificada uma linha duplicada, mas o notebook não a remove.
- Existem famílias com apenas um registro, e a validação cruzada apresenta um aviso sobre classes com menos de cinco exemplos. É necessário definir um tratamento para essas famílias antes de refazer a avaliação.
- A divisão de treino e teste não utiliza estratificação.
- A matriz de confusão mostra apenas 15 famílias e omite os casos que envolvem rótulos fora dessa seleção. Ela não representa todos os erros do modelo.
- Na célula de leitura do CSV, remova os espaços antes de `df = pd.read_csv(...)` para evitar erro de indentação ao executar novamente.

## Tecnologias utilizadas

- Python
- Google Colab
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn

## Como executar

1. Abra o arquivo `ativFishmorphfamily.ipynb` no Google Colab.
2. Ajuste a indentação da linha de leitura do CSV, conforme observado acima.
3. Execute a primeira célula e envie o arquivo `FISHMORPH_Family_Dataset.csv`.
4. Execute as demais células na ordem. Para refazer a avaliação corretamente, aplique os ajustes indicados antes do treinamento.
5. Aguarde a conclusão do GridSearchCV e consulte os resultados e gráficos.

## Arquivos

- `ativFishmorphfamily.ipynb`: notebook com o código e as saídas da análise.
- `FISHMORPH_Family_Dataset.csv`: base de dados utilizada.
- `README.md`: descrição do projeto.

## Autor

Luis Fernando Rubinho Souza

## Disciplina

Inteligência Artificial
