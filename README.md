# Alura Challenge BI
O desafio consiste em desenvolver dashboards de logística, marketing e financeiro, utilizando conceitos de BI, do básico ao avançado, e criar um portfólio na área. Tudo isso durante as quatro semanas propostas no desafio.

## :truck: Semana 1: Logística (Alura Log):
A pessoa que gerencia a área de logística da Alura Log, está enfrentando algumas mudanças em sua área por conta do aumento da demanda dos serviços de logística no período da pandemia. Ela quer manter a qualidade de seu serviço, mas para isso precisa acompanhar constantemente as métricas do seu departamento para tomar as melhores decisões. Quando nos contou isso, analisamos que para auxiliar nesse desafio precisaremos fazer um dashboard para logística. Para isso, vamos visualizar algumas métricas muito importantes para a área.

### Indicadores solicitados:
:heavy_check_mark: Visualizar quantas entregas foram feitas no prazo

:heavy_check_mark: Visualizar quantas entregas foram feitas atrasadas

:heavy_check_mark: Mostrar o número de veículos disponíveis

:heavy_check_mark: Calcular o S2D - Ship to door - expedição até a entrega, medido em dias

:heavy_check_mark: Visualizar o nível médio de estoque por ano

:heavy_check_mark: Mostrar o índice de ocorrências por estado.

### :fast_forward: Etapa 1: ETL
As fontes de dados são 4 planilhas em .csv extraídas para o Power BI através do Power Query. As principais transformações necessárias foram divisão de coluna, substituição de valor, tratamento de datas (formato EUA) e join. Nessa etapa, também são revisados/criados os relacionamentos entre as tabelas carregadas.

![image](https://user-images.githubusercontent.com/90648655/133150865-5f6bf6a3-64ed-4434-befb-6b7a18abba59.png)

### :fast_forward: Etapa 2: criação das medidas (indicadores)
