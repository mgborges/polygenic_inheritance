# polygenic_inheritance
Implementation of AI models to identify a polygenic profile for infantile epileptic encephalopathies


A chamada de variantes de nosso conjunto de dados de 122 pacientes (grupo EEI) com o conjunto de 258 amostras do banco de dados de controles do BIPMed-WES (grupo BIPMED), resultou em 1001319 variantes. Posteriormente, consideramos as variantes com cobertura média superior a 20x, e com qualidade maior que 30 e com mais de 90% das amostras com sequências alinhadas nesta região, resultando em 480188 variantes (47,9% das variantes originais). Dada a manifestação neurológica, também consideramos como filtro as variantes em genes associados ao sistema nervoso (listados no Apêndice B), resultando em 53545 variantes (5,3% das variantes originais). Para os modelos de predição construídos no RapidMiner Studio, excluímos as variantes com uma correlação muito baixa ou muito alta em relação a classificação entre nossos dois grupos (EEI e BIPMED). Este filtro resultou em 6805 variantes (0,7% das variantes originais).

A Figura 10 mostra a comparação das curvas ROC para todos os modelos considerados em nossa análise: Naive Bayes; Modelo Linear generalizado (GLM) (com regularização); Regressão Logística; Fast Large Margin (com optimização automática); Aprendizagem Profunda, “deep-learning”; Árvore de Decisão (com optimização automática); Floresta Aleatória, “random forests” (com optimização automática); Árvores Impulsionadas por Gradiente (XGBoost) (com optimização automática); Support Vector Machine (SVM) (com optimização automática). Quanto mais próxima a curva estiver do canto superior esquerdo, melhor o modelo. A Tabela 9 sumariza algumas métricas para os modelos implementados. Podemos notar que três modelos obtiveram um AUC menor que 0,6: Fast Large Margin, Random Forest e Árvores de decisão. Desta forma, calculamos os pesos de todas as variantes empregadas para os demais modelos. O peso reflete a importância global de cada variante para a predição da classificação entre os grupos de destino (EEI e BIPMED), independente do algoritmo de modelagem.

Diante dos valores de importância para as variantes consideradas para os modelos com AUC da curva ROC maiores que 0,6, selecionamos as variantes com uma importância superior a 0,4, o que resultou em 38 variantes-alvo para refinamento do nosso modelo. Incluímos ao grupo destas 38 variantes, aquelas na vizinhança das alterações em até 500 pares de base e no gene correspondente, resultando em 332 variantes para um segundo modelo, que após considerarmos as variantes com importância maior que 0,4, resultou em 32 variantes (disponíveis em https://github.com/mgborges/polygenic_inheritance/blob/master/EEI_targets.vcf). A Tabela 10 e Figura 11 mostram as métricas para os modelos utilizando estes alvos.

Dentre nossos alvos, identificamos 24 genes correspondentes a estas posições. Utilizamos o ConsensusPathDB-human para realizar as análises sobre representação dos genes considerados. Obtivemos como resultado 72 entradas para o conjunto de genes baseados em vizinhança enriquecidos (NESTs), 3 vias enriquecidas, e 33 entradas de conjuntos baseados em ontologia genética enriquecida. Resultados detalhados desta análise se encontram disponíveis em https://github.com/mgborges/polygenic_inheritance. Dentre as vias enriquecidas, estão: Neurexinas e neuroliginas; Interações proteína-proteína nas sinapses; e Sinapse glutamatérgica.
