# Simulador Financeiro de Manutenção Preditiva

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/HEAD?urlpath=%2Fdoc%2Ftree%2Fsimulador%2Fsimulacao.ipynb)


Este simulador interativo permite avaliar o impacto financeiro da adoção de manutenção preditiva baseada em Machine Learning em comparação com uma estratégia tradicional de manutenção reativa (corretiva).


## Objetivo do Projeto

Este simulador faz parte do projeto Manutenção Preditiva em Máquinas Industriais, cujo objetivo é:

- prever falhas de máquinas utilizando dados de sensores
- aplicar modelos de Machine Learning para detecção antecipada de risco
- avaliar o impacto operacional e financeiro da manutenção preditiva

Além da análise preditiva, o projeto busca demonstrar como resultados de modelos de Machine Learning podem ser traduzidos em métricas de negócio, facilitando a tomada de decisão em ambientes industriais. 
Assim, demonstrar, de forma prática, como o desempenho de um modelo de classificação (neste caso, um modelo XGBoost) pode influenciar diretamente os custos operacionais relacionados a falhas de máquinas industriais.



<div align="center">
  <img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/5ab69250a9985d4f5750229e49267093a4487dc1/images/simulador_pt.png" alt="Widget para Simulação" width="100%" style="display:block;"/>
</div>


A simulação utiliza como base a matriz de confusão obtida no conjunto de testes do modelo, considerando:

- Verdadeiros Positivos (falhas corretamente previstas)
- Falsos Positivos (intervenções desnecessárias)
- Falsos Negativos (falhas não previstas)
- Verdadeiros Negativos

A partir desses resultados, os eventos são normalizados para um período mensal, permitindo estimar:

- número esperado de falhas
- intervenções de manutenção preditiva
- falhas não detectadas

Com base nesses valores, o simulador calcula e compara:

- custo mensal da manutenção reativa
- custo mensal da manutenção preditiva
- benefício financeiro líquido
- retorno sobre investimento (ROI)

O usuário pode ajustar diferentes parâmetros operacionais por meio de controles interativos, como:

- impacto financeiro do downtime por hora
- custo operacional do downtime
- custo da manutenção preditiva
- duração média do downtime
- custo mensal do sistema de machine learning

Isso permite explorar diferentes cenários financeiros e operacionais, avaliando em quais condições a manutenção preditiva se torna economicamente vantajosa.

## Executar o Simulador
Clique no botão abaixo para abrir o notebook interativo diretamente no navegador usando Binder.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/HEAD?urlpath=%2Fdoc%2Ftree%2Fsimulador%2Fsimulacao.ipynb)
