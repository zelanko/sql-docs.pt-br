---
title: "Como criar Consultas MDX usando olapR | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: 3
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# Como criar Consultas MDX usando olapR
## <a name="how-to-build-an-mdx-query-from-r"></a>Como criar uma consulta MDX no R

1. Defina uma cadeia de conexão que especifica a fonte de dados OLAP (instância do SSAS) e o provedor MSOLAP.

2. Use a função `OlapConnection(connectionString)` para criar um identificador para a consulta MDX e transmitir a cadeia de conexão.

3. Use o construtor `Query()` para instanciar um objeto de consulta.

4. Use as seguintes funções auxiliares para fornecer mais detalhes sobre as dimensões e medidas a serem incluídas na consulta MDX:
     + `cube()` Especifique o nome do banco de dados de SSAS.
     + `columns()` Forneça os nomes de medidas para usar no argumento ON COLUMNS.  
     + `rows()` Forneça os nomes de medidas para usar no argumento ON ROWS.
     + `slicers()` Especifique um campo ou membros para usar como uma segmentação de dados. Uma segmentação de dados é como um filtro que é aplicado a todos os dados da consulta MDX.
     
     + `axis()` Especifique o nome de um eixo adicional para usar na consulta. Um cubo OLAP pode conter até 128 eixos de consulta. Em geral, os primeiros quatro eixos são denominados Colunas, Linhas, Páginas e Capítulos. Se sua consulta for relativamente simples, você poderá usar as funções `columns`, `rows`, etc. para criar a consulta.     
     No entanto, você também pode usar a função `axis()` com um valor de índice diferente de zero para criar uma consulta MDX com muitos qualificadores, ou para adicionar dimensões extras como qualificadores.

5. Transmita o identificador e a consulta MDX concluída para as funções `executeMD` ou `execute2D`, dependendo da forma dos resultados.

  + `executeMD` Retorna uma matriz multidimensional
  + `execute2D` Retorna um quadro de dados (tabular) bidimensional


## <a name="how-to-run-an-existing-mdx-query-from-r"></a>Como executar uma consulta MDX existente do R

1. Defina uma cadeia de conexão que especifica a fonte de dados OLAP (instância do SSAS) e o provedor MSOLAP.

2. Use a função `OlapConnection(connectionString)` para criar um identificador para a consulta MDX e transmitir a cadeia de conexão.

3. Defina uma variável de R para armazenar o texto da consulta MDX.

4. Transmita o identificador e a variável que contendo a consulta MDX para as funções `executeMD` ou `execute2D`, dependendo da forma dos resultados.

    + `executeMD` Retorna uma matriz multidimensional
    + `execute2D` Retorna um quadro de dados (tabular) bidimensional



## <a name="examples"></a>Exemplos

### <a name="1-basic-mdx-with-slicer"></a>1. MDX básica com segmentação de dados

Essa consulta MDX seleciona as _medidas_ para a contagem e o valor da contagem de vendas pela Internet e o valor das vendas e as coloca no eixo das Colunas. Ela adiciona um membro da dimensão SalesTerritory como uma *segmentação de dados* para filtrar a consulta de modo que somente as vendas da Austrália sejam usadas nos cálculos.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ Nas colunas, você pode especificar várias medidas como elementos de uma cadeia de caracteres separada por vírgulas.
+ O eixo Linha usa todos os valores possíveis (todos os MEMBROS) da dimensão "Linha de produto". 
+ Essa consulta retornará uma tabela com três colunas contendo um resumo _acumulado_ de vendas pela Internet de todos os países. 
+ A cláusula WHERE é o _eixo da segmentação_. A segmentação de dados adiciona um membro da dimensão SalesTerritory para filtrar a consulta de modo que somente as vendas da Austrália sejam usadas nos cálculos.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>Para criar essa consulta usando as funções fornecidas em olapR

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>Para executar essa consulta como uma cadeia de caracteres MDX predefinida

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Observe que se você definir uma consulta usando o construtor MDX no SQL Server Management Studio e, em seguida, salvar a cadeia de caracteres MDX, ele numerará os eixos começando em 0, conforme mostrado aqui: 

~~~~
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Country].[Australia]
~~~~

Você ainda pode executar essa consulta como uma cadeia de caracteres MDX predefinida. No entanto, para criar a mesma consulta usando o R com a função `axis()`, não se esqueça de numerar os eixos começando em 1.


### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Explore os cubos e seus campos em uma instância do SSAS

Você pode usar a função `explore` para retornar uma lista de cubos, dimensões ou membros para usar na construção de sua consulta. Isso é útil se você não tiver acesso a outras ferramentas de procura em OLAP ou se você quiser manipular programaticamente ou construir a consulta MDX.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>Para listar os cubos disponíveis na conexão especificada

Para exibir todos os cubos ou perspectivas na instância que você tem permissão para exibir, forneça o identificador como um argumento para `explore`.
Observe que o resultado final não é um cubo; TRUE indica apenas que a operação de metadados foi bem-sucedida. Um erro será gerado se os argumentos forem inválidos.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| Resultados  |  
| ----|
| _Tutorial do Analysis Services_|
|_Vendas pela Internet_|
|_Vendas do revendedor_|
|_Resumo de vendas_|
|_[1] TRUE_|
     


#### <a name="to-get-a-list-of-cube-dimensions"></a>Para obter uma lista de dimensões do cubo

Para exibir todas as dimensões no cubo ou perspectiva, especifique o nome do cubo ou da perspectiva.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| Resultados  |  
| ----|
| _Cliente_|
|_Data_|
|_Região_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>Para retornar todos os membros da dimensão e hierarquia especificada

Depois de definir a fonte e criar o identificador, especifique o cubo, a dimensão e a hierarquia a serem retornados.
Observe que os itens nos resultados retornados que têm prefixo **->** representam os filhos do membro anterior.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| Resultados  |  
| ----|
| _Acessórios_|
|_Bicicletas_|
|_Roupas_|
|_Componentes_|
|-> Componentes do assembly|
|-> Componentes do assembly|



## <a name="see-also"></a>Consulte também

[Usando dados de cubos OLAP no R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)