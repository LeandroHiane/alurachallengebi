# Alura Challenge BI
O desafio consiste em desenvolver dashboards de logística, marketing e financeiro, utilizando conceitos de BI, do básico ao avançado, e criar um portfólio na área. Tudo isso durante as quatro semanas propostas no desafio.

[Semana 1: Logística]
[Semana 2: Marketing]
[Semana 3 e 4: Financeiro]

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

Capa do dashboard:

![image](https://user-images.githubusercontent.com/90648655/133153561-028d44cc-084c-4324-a3c1-524363c85175.png)

:heavy_check_mark: Plus! Adicionado o indicador da quantidade de pedidos atrasados.

Detalhe da tooltip para os veículos disponíveis:

![image](https://user-images.githubusercontent.com/90648655/133154258-547a5605-711d-48d0-9c00-22452a8f98b7.png)

### :fire: Plus!
Além dos indicadores solicitados, uma página adicional com informações gerenciais foi criada para proporcionar insights ao negócio.

:heavy_check_mark: Receita total dos pedidos + tabela ordenada pelas categorias de produtos que mais geraram receita.

:heavy_check_mark: Quantidade total dos produtos entregues + tabela ordenada pelas categorias de produtos com maior quantidade entregue.

:heavy_check_mark: Distribuição da quantidade de pedidos pelo modal de transporte utilizado.

![image](https://user-images.githubusercontent.com/90648655/133155611-02fd2184-bce7-4478-8252-e63e2aada43c.png)


## :shopping_cart: Semana 2: Marketing (Alura Shop):
Agora a Alura Shop investiu em publicidade para se destacar no mercado, e a gerência da empresa tem dúvidas se o retorno dessa propaganda surtiu efeito. A nossa missão é apoiar a gerência em suas tomadas de decisão, e elucidar as dúvidas. Para isso desenvolveremos um dashboard estratégico de marketing com o objetivo de monitorar uma campanha de publicidade paga durante o mês de julho de 2021. Apresentaremos indicadores relevantes para a validação estratégica do negócio.

### Indicadores solicitados:
:heavy_check_mark: Calcular o total de compras

:heavy_check_mark: Calcular o total de valor convertido em compras

:heavy_check_mark: Mostrar o total do valor investido na campanha

:heavy_check_mark: Calcular o custo por clique

:heavy_check_mark: Exibir a jornada de compra

:heavy_check_mark: Calcular a taxa de conversão

:heavy_check_mark: Mostrar o ticket médio por dispositivo

:heavy_check_mark: Mostrar Retorno do investimento em publicidade (ROAS) por idade e gênero

:heavy_check_mark: Calcular o valor convertido em compras por dia

Além disso, foi solicitado que o dashboard tivesse atualizações em dias úteis às 9h e a exibição do horário da atualização.

### :fast_forward: Etapa 1: ETL
As fontes de dados são 2 arquivos em .json extraídos para o Power BI através do Power Query. Não foram necessárias grandes manipulações nos arquivos, somente pequenas alterações de transformações de textos e filtros dos dados. Também não foi necessário criar uma relação entre as tabelas.

### :fast_forward: Etapa 2: criação das medidas (indicadores)
Medidas criadas:

Medida | Fórmula
------------ | -------------
CPC | DIVIDE(SUM(Tabela_idade_e_genero[Quantia gasta (BRL)]), SUM(Tabela_idade_e_genero[Cliques no link]))
Conversão em compras | DIVIDE(SUM(Tabela_idade_e_genero[Compras]), SUM(Tabela_idade_e_genero[Cliques no link]))
Ticket Médio | DIVIDE(SUM(Tabela_dispositivos[Quantia gasta (BRL)]), SUM(Tabela_dispositivos[Compras]))
ROAS | DIVIDE(SUM(Tabela_idade_e_genero[Valor de conversão de compras]), SUM(Tabela_idade_e_genero[Quantia gasta (BRL)]))

### :fast_forward: Etapa 3: montagem do dashboard
O esquema de cores utilizado foi o Daltônico (nativo do pBI), buscando por bastante contraste entre as informações, os gráficos e o background com o objetivo de tornar o dashboard acessível.

O dashboard foi dividido em duas páginas, sendo a primeira com a Visão Compras:

![image](https://user-images.githubusercontent.com/90648655/134400501-fb06928d-bc0b-4405-8203-f891641c2855.png)

E a segunda com a Visão Custos e Retorno:

![image](https://user-images.githubusercontent.com/90648655/134400623-79efa22e-8b33-457a-8ee2-46e5cc0bf43d.png)

### :fire: Plus!
:heavy_check_mark: Dois visuais foram adicionados na Visão Compras para acrescentar informações nas tomadas de decisões:

![image](https://user-images.githubusercontent.com/90648655/134402536-04fe9fb5-d548-4c89-ab8a-d9dd35ee5832.png)

:bulb: O Facebook está morrendo, certo? Para a Alura Shop: **não**! Esta é a plataforma que mais converte em compras através dos anúncios. Definir corretamente a **praça** (alô, Ps do Marketing!) de distribuição dos anúncios é fundamental para uma melhor conversão.

:bulb: Além disso, o dados mostram que os anúncios exibidos no **feed** são a melhor opção para conversão. Capriche no copy e no design desse formato!

:heavy_check_mark: Na Visão Custos e Retorno, foi adicionado o indicador ROAS total, pois não faz sentido vê-lo apenas quebrado por idade e gênero. Além disso, ver o custo quebrado por dia auxilia no entendimento das sazonalidades, que podem indicar aumento de cliques por parte dos usuários, aumento da concorrência elevando o CPC, etc.

![image](https://user-images.githubusercontent.com/90648655/134403644-14e3f197-de4e-4bf9-9f97-798305079a71.png)
