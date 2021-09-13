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
Algumas colunas adicionais foram criadas com DAX para facilitar os cálculos das medidas, como abaixo:

![image](https://user-images.githubusercontent.com/90648655/133151343-b572ce33-6598-40fe-bc97-123ed95df4d4.png)

Medidas criadas:
Medida | Fórmula
------------ | -------------
% Entregas realizadas dentro do prazo | DIVIDE([Entregas realizadas dentro do prazo],[Entregas realizadas])
% Entregas realizadas fora do prazo | DIVIDE([Entregas realizadas fora do prazo],[Entregas realizadas])
% Receita pedidos acumulados | DIVIDE([Receita pedidos acumulado],CALCULATE([Receita pedidos],ALL(Pedidos[Desc Produto])))
Entregas realizadas | CALCULATE(COUNT(Pedidos[ID Pedido]),Pedidos[Status do pedido] = "Entregue")
Entregas realizadas dentro do prazo | CALCULATE(COUNT(Pedidos[Entrega dentro do prazo]),Pedidos[Entrega dentro do prazo] = 1)
Entregas realizadas fora do prazo | CALCULATE(COUNT(Pedidos[Entrega dentro do prazo]),Pedidos[Entrega dentro do prazo] = 0)
Pedidos atrasados | CALCULATE(COUNT(Pedidos[ID Pedido]),Pedidos[Pedido atrasado] = 1)
Qtde veiculos disponiveis | CALCULATE(COUNT(Veiculos[ID Veículo]),Veiculos[Status] = "Disponível")
Quantidade produtos | SUM(Pedidos[Quantidade])
Ranking produtos quantidade | RANKX(ALL(Pedidos[Desc Produto]),[Quantidade produtos])
Ranking produtos receita pedidos | RANKX(ALL(Pedidos[Desc Produto]),[Receita pedidos])
Receita pedidos | SUM(Pedidos[Receita pedido])
Receita pedidos acumulado | CALCULATE([Receita pedidos],TOPN([Ranking produtos receita pedidos],ALL(Pedidos[Desc Produto]),[Receita pedidos],DESC))

### :fast_forward: Etapa 3: montagem do dashboard
O esquema de cores utilizado foi o Daltônico (nativo do pBI), buscando por bastante contraste entre as informações, os gráficos e o background com o objetivo de tornar o dashboard acessível.

![image](https://user-images.githubusercontent.com/90648655/133153561-028d44cc-084c-4324-a3c1-524363c85175.png)

