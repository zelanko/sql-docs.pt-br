---
title: 'Início Rápido: Estruturas de dados, tipos de dados e objetos de R'
titleSuffix: SQL machine learning
description: Neste início rápido, você aprenderá a usar estruturas de dados, tipos de dados e objetos ao usar R no aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5b5f4e90b680f5ae06944eedc997a43b8a40024
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606558"
---
# <a name="quickstart-data-structures-data-types-and-objects-using-r-with-sql-machine-learning"></a>Início Rápido: Estruturas de dados, tipos de dados e objetos usando o R com o aprendizado de máquina do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar estruturas de dados e tipos de dados ao usar R nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). Você aprenderá como mover dados entre o R e o SQL Server e os problemas comuns que podem ocorrer.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar estruturas de dados e tipos de dados ao usar R nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Você aprenderá como mover dados entre o R e o SQL Server e os problemas comuns que podem ocorrer.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Neste início rápido, você aprenderá a usar estruturas de dados e tipos de dados ao usar R no [SQL Server R Services](../r/sql-server-r-services.md). Você aprenderá como mover dados entre o R e o SQL Server e os problemas comuns que podem ocorrer.
::: moniker-end

Os problemas comuns que se deve conhecer de antemão incluem:

- Os tipos de dados às vezes não correspondem
- Conversões implícitas podem ocorrer
- Às vezes, operações de conversão são necessárias
- R e SQL usam objetos de dados diferentes

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- SQL Server 2016 R Services. Para saber como instalar o R Services, confira o [Guia de instalação do Windows](../install/sql-r-services-windows-install.md). 
::: moniker-end

- Uma ferramenta para executar consultas SQL que contenham scripts do R. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="always-return-a-data-frame"></a>Sempre retornar uma estrutura de dados

Quando o script retorna resultados de R para o SQL Server, ele deve retornar os dados como um **data.frame**. Qualquer outro tipo de objeto gerado no seu script, seja uma lista, fator, vetor ou dados binários, deverá ser convertido em uma estrutura de dados se você desejar enviá-lo como parte dos resultados do procedimento armazenado. Felizmente, existem várias funções de R para dar suporte à conversão de outros objetos em um quadro de dados. É possível até mesmo serializar um modelo binário e retorná-lo em uma estrutura de dados, o que faremos posteriormente neste início rápido.

Primeiro, vamos experimentar alguns objetos básicos de R (vetores, matrizes e listas) e ver como a conversão em uma estrutura de dados muda a saída passada para o SQL Server.

Compare esses dois scripts "Olá, Mundo" em R. Os scripts parecem quase idênticos, mas o primeiro retorna uma única coluna de três valores, enquanto o segundo retorna três colunas com um único valor cada.

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

## <a name="identify-schema-and-data-types"></a>Identificar tipos de dados e esquema

Por que os resultados são tão diferentes?

A resposta geralmente pode ser encontrada usando o comando `str()` de R. Adicione a função `str(object_name)` em qualquer ponto do script R para fazer com que o esquema de dados do objeto R especificado seja retornado como uma mensagem informativa.

Para descobrir por que os exemplos 1 e 2 apresentam resultados tão diferentes, insira a linha `str(OutputDataSet)` no final da definição de variável `@script` em cada instrução, dessa forma:

**Exemplo 1 com a função str adicionada**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Exemplo 2 com a função str adicionada**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

Agora, examine o texto em **Mensagens** para ver por que a saída é diferente.

**Resultados – Exemplo 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Resultados – Exemplo 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Como você pode ver, uma pequena alteração na sintaxe de R teve um grande efeito no esquema dos resultados. Não entraremos no porquê, mas as diferenças nos tipos de dados de R são explicadas mais detalhadamente na seção *Estruturas de Dados* no artigo ["Advanced R" (R Avançado) de Hadley Wickham](http://adv-r.had.co.nz).

Por enquanto, apenas esteja ciente de que você precisa verificar os resultados esperados ao moldar objetos R em quadros de dados.

> [!TIP]
> Você também pode usar funções de identidade do R, tais como `is.matrix` e `is.vector`, para retornar informações sobre a estrutura de dados interna.

## <a name="implicit-conversion-of-data-objects"></a>Conversão implícita de objetos de dados

Cada objeto de dados R tem suas próprias regras para o modo como os valores são manipulados quando combinados com outros objetos de dados se os objetos de dados têm o mesmo número de dimensões ou se qualquer objeto de dados contém tipos de dados heterogêneos.

Primeiro, crie uma pequena tabela de dados de teste.

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)

INSERT INTO RTestData
VALUES (1);

INSERT INTO RTestData
VALUES (10);

INSERT INTO RTestData
VALUES (100);
GO
```

Por exemplo, suponha que você execute a seguinte instrução para realizar uma multiplicação de matriz usando R. Multiplique uma matriz de coluna única com os três valores de uma matriz com quatro valores, esperando uma matriz de 4x3 como resultado.

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
|1200|1300|1\.400|1500|

No entanto, observe o que acontece quando você altera o tamanho da matriz `y`.

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

Por quê? Nesse caso, como os dois argumentos podem ser tratados como vetores de mesmo tamanho, R retorna o produto interno como uma matriz.  Esse é o comportamento esperado de acordo com as regras de álgebra linear; no entanto, isso pode causar problemas se seu aplicativo downstream espera que o esquema de saída nunca mude.

> [!TIP]
> 
> Encontrou erros? Verifique se você está executando o procedimento armazenado no contexto do banco de dados que contém a tabela, não no **mestre** nem em outro banco de dados.
>
> Além disso, sugerimos que você evite usar tabelas temporárias para esses exemplos. Alguns clientes do R encerrarão uma conexão entre os lotes, excluindo tabelas temporárias.

## <a name="merge-or-multiply-columns-of-different-length"></a>Mesclar ou multiplicar colunas de tamanhos diferentes

O R fornece uma ótima flexibilidade para trabalhar com vetores de tamanhos diferentes e combinar essas estruturas semelhantes a colunas em estruturas de dados. Listas de vetores podem se parecer com uma tabela, mas elas não seguem as regras que regem as tabelas de banco de dados.

Por exemplo, o script a seguir define uma matriz numérica de tamanho 6 e a armazena na variável `df1` de R. Em seguida, a matriz numérica é combinada com os inteiros da tabela RTestData, que contém três (3) valores, para criar uma estrutura de dados, `df2`.

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

## <a name="cast-or-convert-data"></a>Converter dados

O R e o SQL Server não usam os mesmos tipos de dados, por isso quando você executa uma consulta no SQL Server para obter dados e passa-os para o runtime de R, geralmente ocorre um certo tipo de conversão implícita. Outro conjunto de conversões ocorre quando você retorna dados de R para o SQL Server.

- O SQL Server envia os dados da consulta para o processo do R gerenciado pelo serviço do Launchpad e converte-os em uma representação interna para maior eficiência.
- O runtime do R carrega os dados em uma variável data.frame e executa suas próprias operações nos dados.
- O mecanismo de banco de dados retorna os dados para o SQL Server usando uma conexão interna protegida e apresenta os dados em termos de tipos de dados do SQL Server.
- Você obtém os dados conectando-se ao SQL Server usando uma biblioteca de cliente ou de rede que pode emitir consultas SQL e lidar com conjuntos de dados tabulares. Esse aplicativo cliente pode afetar os dados de outras maneiras.

Para ver como isso funciona, execute uma consulta como no data warehouse [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Essa exibição retorna dados de vendas usados na criação de previsões.

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
>
> Você pode usar qualquer versão do AdventureWorks ou criar uma consulta diferente usando um banco de dados próprio. O ponto aqui é tentar manipular alguns dados que contêm texto, data e hora e valores numéricos.

Agora, tente colar essa consulta como a entrada para o procedimento armazenado.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Se você receber um erro, provavelmente precisará fazer algumas modificações no texto da consulta. Por exemplo, predicado de cadeia de caracteres na cláusula WHERE deve estar entre dois conjuntos de aspas simples.

Depois de fazer a consulta funcionar, examine os resultados da função `str` para ver como R trata os dados de entrada.

**Resultados**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

- A coluna datetime foi processada usando o tipo de dados de R, **POSIXct**.
- A coluna de texto "ProductSeries" foi identificada como um **fator**, o que significa uma variável categórica. Valores de cadeia de caracteres são tratados como fatores por padrão. Se você passar uma cadeia de caracteres R, ele será convertida em um inteiro para uso interno e, em seguida, mapeada para cadeia de caracteres na saída.

### <a name="summary"></a>Resumo

Com base até mesmo nesses pequenos exemplos, você pode ver a necessidade de verificar os efeitos da conversão de dados ao passar consultas SQL como entrada. Devido a alguns tipos de dados do SQL Server não serem compatíveis com o R, considere os seguintes modos de evitar erros:

- Teste os dados com antecedência e verifique as colunas ou valores em seu esquema que poderiam ser um problema ao ser passados para o código R.
- Especifique as colunas na fonte de dados de entrada individualmente, em vez de usar `SELECT *` e saiba como cada coluna será tratada.
- Execute conversões explícitas conforme necessário durante a preparação dos dados de entrada, a fim de evitar surpresas.
- Evite passar colunas de dados (como GUIDs ou rowguids) que causam erros e não são úteis para modelagem.

Para obter mais informações sobre os tipos de dados compatíveis e não compatíveis, confira [Tipos de dados e bibliotecas do R](../r/r-libraries-and-data-types.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como escrever funções avançadas do R com o aprendizado de máquina do SQL, siga este início rápido:

> [!div class="nextstepaction"]
> [Escrever funções avançadas do R com o aprendizado de máquina do SQL](quickstart-r-functions.md)
