---
title: "R e SQL dados e tipos de objetos de dados (R no início rápido do SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4207d26b2f38e3f13a45c21ab40293cf0dc95219
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R e SQL dados e tipos de objetos de dados (R no início rápido do SQL)

Nesta etapa, você aprenderá sobre alguns problemas comuns que podem surgir ao mover dados entre R e SQL Server:

+ Os tipos de dados às vezes não coincidem
+ Conversões implícitas podem ocorrer
+ Às vezes, operações de conversão são necessárias
+ R e SQL usam objetos de dados diferentes

## <a name="always-return-r-data-as-a-data-frame"></a>Sempre retornar dados R como um quadro de dados

Quando o script retorna resultados de R para o SQL Server, ele deve retornar os dados como um **data.frame**. Qualquer outro tipo de objeto gerado no seu script, seja uma lista, fator, vetor ou dados binários, deverá ser convertido em um quadro de dados se você desejar enviá-lo como parte dos resultados do procedimento armazenado. Felizmente, existem várias funções de R para dar suporte à conversão de outros objetos em um quadro de dados. É possível até mesmo serializar um modelo binário e retorná-lo em um quadro de dados, o que faremos posteriormente neste tutorial.

Primeiro, vamos fazer experiências com alguns objetos de R básicos do R — vetores, matrizes e listas — e ver como a conversão em um quadro de dados altera a saída passada para o SQL Server.

Comparar esses dois scripts "Hello World" em R. Os scripts parecem quase idênticos, mas o primeiro retorna uma única coluna de três valores, enquanto o segundo retorna três colunas com um único valor de cada um.

**Exemplo 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**Exemplo 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>Identificando os tipos de dados e esquema de dados R

Por que os resultados são tão diferentes?

A resposta geralmente pode ser encontrada usando o comando `str()` de R. Adicione a função `str(object_name)` em qualquer ponto do script R para fazer com que o esquema de dados do objeto R especificado seja retornado como uma mensagem informativa. Para exibir mensagens, consulte o painel **Mensagens** do código do Visual Studio ou a guia **Mensagens** no SSMS.

Para descobrir por que os exemplos 1 e 2 demonstram resultados tão diferentes, insira a linha `str(OutputDataSet)` no final da definição de variável  _@script_  em cada instrução, dessa forma:

**Exemplo 1 com a função str adicionado**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Exemplo 2 com a função str adicionado**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet)' , 
  @input_data_1 = N'  ';
```

Agora, examine o texto em **Mensagens** para ver por que a saída é diferente.

**Resultados – Exemplo 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Resultados – Exemplo 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Como você pode ver, uma pequena alteração na sintaxe de R teve um grande efeito no esquema dos resultados. Não vamos entrar porque, porque as diferenças nos tipos de dados de R são explicadas mais detalhadamente neste artigo por Hadley Wickham: [estruturas de dados R](http://adv-r.had.co.nz/Data-structures.html).

Por enquanto, apenas esteja ciente de que você precisa verificar os resultados esperados ao moldar objetos R em quadros de dados.

> [!TIP]
> 
> Você também pode usar funções de identidade de R, como `is.matrix`, `is.vector`, etc.

## <a name="implicit-conversion-of-data-objects"></a>Conversão implícita de objetos de dados

Cada objeto de dados R tem suas próprias regras para como os valores são manipulados quando combinado com outros objetos de dados se os objetos de dados têm o mesmo número de dimensões ou se qualquer objeto de dados contém tipos de dados heterogêneos.

Por exemplo, suponha que você execute a seguinte instrução para realizar uma multiplicação de matriz usando R. Multiplique uma matriz de coluna única com os três valores de uma matriz com quatro valores, esperando uma matriz de 4 x 3 como resultado.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

Nos bastidores, a coluna de três valores é convertida em uma matriz de coluna única. Como uma matriz é apenas um caso especial de uma matriz de R, a matriz `y` é implicitamente moldada em uma matriz de coluna única para que os dois argumentos estejam em conformidade.

**Resultados**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

No entanto, observe o que acontece quando você alterar o tamanho da matriz `y`.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

Agora, R retorna um único valor como resultado.

**Resultados**
    
|Col1|
|---|
|1542|

Por quê? Nesse caso, porque os dois argumentos podem ser tratados como vetores do mesmo tamanho, R retorna o produto de interna como uma matriz.  Esse é o comportamento esperado de acordo com as regras de álgebra linear; no entanto, isso pode causar problemas se seu aplicativo downstream espera que o esquema de saída nunca mude.

> [!TIP]
> 
> Recebendo erros? Esses exemplos exigem a tabela **RTestData**. Se você não criou a tabela de dados de teste, volte para este tópico: [trabalhando com entradas e saídas](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Se você criou a tabela, mas ainda receber um erro, certifique-se de que você está executando o procedimento armazenado no contexto do banco de dados que contém a tabela e não no **mestre** ou outro banco de dados.
> 
> Além disso, sugerimos que você evite usar tabelas temporárias para esses exemplos. Alguns clientes R terminará uma conexão entre os lotes, excluindo tabelas temporárias.

## <a name="merge-or-multiply-columns-of-different-length"></a>Mesclar ou multiplicar colunas de tamanhos diferentes

R fornece uma grande flexibilidade para trabalhar com vetores de tamanhos diferentes e para combinar essas estruturas de coluna em quadros de dados. Listas de vetores podem se parecer com uma tabela, mas elas não seguem as regras que regem as tabelas de banco de dados.

Por exemplo, o script a seguir define uma matriz numérica de tamanho 6 e a armazena na variável `df1` de R. A matriz numérica é combinado com os inteiros da tabela RTestData, que contém valores de três (3), para tornar um novo quadro de dados, `df2`.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

Para preencher o quadro de dados, R repete os elementos recuperados do RTestData quantas vezes forem necessárias para corresponder ao número de elementos na matriz `df1`.

**Resultados**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

Lembre-se que um quadro de dados somente se parece com uma tabela e é, na verdade, uma lista de vetores.

## <a name="cast-or-convert-sql-server-data"></a>Converter dados do SQL Server

O R e o SQL Server não usam os mesmos tipos de dados, por isso quando você executa uma consulta no SQL Server para obter dados e passa-os para o tempo de execução de R, geralmente ocorre um certo tipo de conversão implícita. Outro conjunto de conversões ocorre quando você retorna dados de R para o SQL Server.

- SQL Server envia os dados da consulta para o processo de R gerenciado pelo serviço de barra inicial e o converte em uma representação interna para maior eficiência.
- O tempo de execução do R carrega os dados em uma variável data.frame e executa suas próprias operações nos dados.
- O mecanismo de banco de dados retorna os dados para o SQL Server usando uma conexão interna protegida e apresenta os dados em termos de tipos de dados do SQL Server.
- Você obtém os dados conectando-se ao SQL Server usando uma biblioteca de cliente ou de rede que pode emitir consultas SQL e lidar com conjuntos de dados tabulares. Esse aplicativo cliente pode afetar os dados de outras maneiras.

Para ver como isso funciona, execute uma consulta como no depósito de dados AdventureWorksDW. Essa exibição retorna dados de vendas usados na criação de previsões.

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> Você pode usar qualquer versão do AdventureWorks, ou criar uma consulta diferente usando um banco de dados de sua preferência. O ponto é tentar manipular alguns dados que contém texto, data e hora e valores numéricos.

Agora, tente colar essa consulta como entrada para o procedimento armazenado.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Se você receber um erro, provavelmente precisará fazer algumas modificações no texto da consulta. Por exemplo, predicado de cadeia de caracteres na cláusula WHERE deve estar entre dois conjuntos de aspas simples.

Depois de fazer a consulta funcionar, examine os resultados da função `str` para ver como R trata os dados de entrada.

**Resultados**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ A coluna datetime foi processada usando o tipo de dados de R, **POSIXct**.
+ A coluna de texto "ProductSeries" foi identificado como um **fator**, que significa que uma variável categórica. Valores de cadeia de caracteres são tratados como fatores por padrão. Se você passar uma cadeia de caracteres R, ele será convertida em um inteiro para uso interno e, em seguida, mapeada para cadeia de caracteres na saída.

### <a name="summary"></a>Resumo

Mesmo que esses exemplos curtos, você pode ver a necessidade de verificar os efeitos da conversão de dados ao passar SQL consultas como entrada. Porque não há suporte para alguns tipos de dados do SQL Server R, considere essas formas de evitar erros:

+ Testar seus dados com antecedência e verifique se a colunas ou valores em seu esquema que pode ser um problema quando passado para código R.
+ Especifique as colunas na fonte de dados de entrada individualmente, em vez de usar `SELECT *` e saiba como cada coluna será tratada.
+ Execute conversões explícitas conforme necessário durante a preparação dos dados de entrada, a fim de evitar surpresas.
+ Evite colunas de passagem de dados (como GUIDS ou rowguids) que causam erros e não são úteis para modelagem.

Para obter mais informações sobre tipos de dados com e sem suporte, consulte [tipos de dados e bibliotecas de R](../r/r-libraries-and-data-types.md).

Para obter informações sobre o impacto no desempenho de tempo de execução conversão de cadeias de caracteres numéricos fatores, consulte [o ajuste de desempenho do SQL Server R Services](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-lesson"></a>Próxima lição

Na próxima etapa, você aprenderá como aplicar funções R aos dados do SQL Server.

[Usando funções de R com os dados do SQL Server](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
