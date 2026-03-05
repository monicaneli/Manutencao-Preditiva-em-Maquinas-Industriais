# Predição de Falhas em Máquinas Industriais

## Contexto do Projeto

Utilizando um dataset do Kaggle, foi considerado o seguinte cenário: na fabricação de componentes metálicos de alta precisão utilizados nos setores aeroespacial, automotivo e de dispositivos médicos, três máquinas distintas operam produzindo peças de diferentes dimensões. A minimização de downtime é crítica para o cumprimento de prazos e eficiência operacional. Com o objetivo de substituir a abordagem reativa por uma estratégia orientada por dados, a empresa passou a coletar dados operacionais ao longo de um ano, registrando ocorrências de parada das máquinas.

Sendo assim, este projeto representa o primeiro passo na utilização desses dados para:

* Aumentar a confiabilidade das máquinas
* Otimizar estratégias de manutenção
* Reduzir impactos financeiros decorrentes de downtime

O projeto está disponível para visualização, comentários e sugestões no meu perfil do Kaggle: [clique aqui](https://www.kaggle.com/code/monicaneli/industrial-machine-downtime-prediction)

---

## 🎯 Objetivos

* **Análise Exploratória (EDA):** Identificar padrões e causas principais das falhas.
* **Modelagem Preditiva:** Antecipar downtime por meio de Machine Learning.
* **Simulação Financeira:** Avaliar viabilidade econômica da manutenção preditiva.
* **Monitoramento:** Definir estratégias para acompanhamento contínuo e melhoria do modelo.

---

## Principais Resultados

### 1️⃣ Qualidade e Coleta de Dados

* Em geral as 3 máquinas apresentaram padrões semelhantes de funcionamento operacional.
* Boa qualidade geral (sem duplicidades e baixo volume de dados ausentes).
* Correlações em valores faltantes sugerem sensores compartilhados ou fatores operacionais comuns.
* Inconsistências temporais na coleta entre máquinas.
* Indícios de possíveis falhas de sensor (valores negativos, extremos ou próximos de zero em Spindle Vibration, Tool Vibration e Torque).
* Necessidade de padronização na coleta e investigação de lacunas.

<div align="center">
	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/weekly.png" alt="Dados e evolução semanal" width="100%" style="display:block;"/>
</div>

---

### 2️⃣ Frequência e Tendência de Downtime
* O número de ocorrências de downtime aumentou durante o período com pico em Março e Abril, e em seguida houve uma queda.
* O número médio de ocorrências de downtime diários foi de aproximadamente 2-3 eventos por dia, por máquina. Porém, houve dias com picos de até 12 eventos em um único dia.
* Em 48 dias, hove uma ou mais máquinas com 100% de downtime.
* Número de linhas de montagem com 100% de tempo de inatividade no mesmo dia: 2 máquinas/linhas de montagem.
* Downtime ocorreu praticamente toda semana.
* Apenas duas semanas sem ocorrência no período analisado.
* Taxa média de downtime próxima de 50% entre as máquinas.
* Sábados apresentaram 100% de ocorrência.


Comparação entre máquinas:

| Máquina                             | Downtime Médio | Leituras Totais | Dias com 100% Downtime |
| ----------------------------------- | -------------- | --------------- | ---------------------- |
| Makino-L1-Unit1-2013 (ShopFloor-L1) | 54%            | 874             | 22                     |
| Makino-L3-Unit1-2015 (ShopFloor-L3) | 51%            | 818             | 19                     |
| Makino-L2-Unit1-2015 (ShopFloor-L2) | 46%            | 808             | 17                     |

---

### 3️⃣ Principais Fatores Associados ao Downtime

Análise estatística e modelo identificaram como principais variáveis:

* 🔻 Menor pressão hidráulica (forte associação)
* 🔻 Menor torque
* 🔺 Maior força de corte
* 🔺 Temperatura do fluido e rotação do spindle (efeito moderado)

<div align="center">
	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/indicadores.png" alt="Fatores associados ao downtime" width="60%" style="display:block;"/>
</div>

---

## Modelagem Preditiva

Foram testados dois modelos: Regressão Logística e XGBoost. Sendo que o modelo **XGBoost** apresentou desempenho superior:

* Accuracy: 99.9%
* F1-score: ~99%
* PR-AUC: 0.991 (vs 0.899 na Regressão Logística)

<div align="center">
	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/avaliacao.png" alt="Avaliação e comparação dos modelos" width="100%" style="display:block;"/>
</div>

Importância das variáveis:

* Hydraulic Pressure (~40%)
* Torque (~25%)
* Cutting (~25%)

Análise SHAP confirmou a relevância de Torque, Cutting, Coolant Pressure e Hydraulic Pressure.

<div align="center">
	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/shap.png" alt="SHapley Additive Explanations" width="60%" style="display:block;"/>
</div>
---

## Simulação Financeira

Foi realizada uma simulação comparando:

* Manutenção Corretiva (Reativa)
* Manutenção Preditiva baseada no modelo

A simulação utilizou:

* 136 dias distintos do conjunto de teste
* Normalização para horizonte mensal
* Custos por hora de produção e manutenção
* Custo operacional mensal do modelo (sem CAPEX inicial)

## Resultados

A simulação indica que, sob as premissas adotadas e considerando um modelo com F1-score de 99%, a manutenção preditiva é financeiramente superior à estratégia reativa na maioria dos cenários testados.

⚠️ Observação importante:
O ROI obtido tende a ser elevado devido a:

* Performance quase perfeita do modelo
* Alta frequência de falhas observada
* Estrutura simplificada de custos
* Exclusão de custos de desenvolvimento e integração

Uma implementação real exigiria:

* Inclusão de lead time mínimo acionável
* Definição de threshold operacional
* Consideração de redução parcial de severidade
* Comparação com manutenção programada
* Inclusão de custos completos de implementação

<div align="center">
	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/simulacao.png" alt="Widget para Simulação" width="58%" style="display:inline-block;"/>
  	<img src="https://github.com/monicaneli/Manutencao-Preditiva-em-Maquinas-Industriais/blob/f097cba3f533654e6a22e384f40ff2b80d921d18/images/resultado.png" alt="Resultado da Simulação ao lado" width="39%" style="display:inline-block; margin-right:10px;"/>
</div>

---

## Próximos Passos

* Investigar confiabilidade dos sensores
* Padronizar coleta de dados
* Aplicar engenharia de features temporais
* Implementar monitoramento em tempo real
* Realizar análise de sensibilidade financeira
* Comparar manutenção corretiva, preditiva e programada

---

## Tecnologias Utilizadas

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* SHAP
* Matplotlib / Seaborn

---

## Conclusão 

O projeto demonstra como a aplicação estruturada de Data Science pode transformar dados operacionais em decisões estratégicas. A modelagem preditiva mostrou alto potencial para redução de downtime e geração de valor financeiro, embora análises adicionais e maior robustez operacional sejam necessárias para implementação industrial em larga escala.

_Thanks for reading!_

