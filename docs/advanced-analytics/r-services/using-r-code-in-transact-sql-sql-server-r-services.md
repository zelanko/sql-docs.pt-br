---
title: "Usando o c&#243;digo do R no Transact-SQL (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# Usando o c&#243;digo do R no Transact-SQL (SQL Server R Services)
Este tutorial fornece exemplos muito breves da sintaxe para trabalhar com o R no SQL Server R Services.    
    
    
Este é um bom ponto para começar se você não estiver familiarizado com o SQL Server R Services e quiser saber mais sobre os conceitos básicos de como definir scripts do R em um procedimento armazenado do T-SQL, como usar dados como entrada e como definir saídas.    
    
**Pré-requisitos:** para executar o código do R no SQL Server R Services, você deve estar conectado a uma instância do SQL Server na qual o R Services já esteja instalado.     
    
## Parte 1 – Operações básicas  

Nas seções a seguir, você aprenderá a estender o procedimento armazenado adicionando parâmetros e a configurar as entradas e saídas.   
  
### 1.1. Verificar se o R está funcionando no SQL Server  

Essa consulta usa o procedimento armazenado do sistema [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx), que é a forma como o R é chamado no contexto do SQL Server. Este exemplo passa uma consulta SQL como entrada para o R, e o R retorna esse quadro de dados para o SQL Server.     
    
1. No Menu Iniciar do Windows, localize o Microsoft SQL Server Management Studio.     
2. Se você não conseguir encontrá-lo, talvez seja necessário instalá-lo: [Baixar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).    
3. Na caixa de diálogo **Conectar ao Servidor**, digite o nome de um servidor ou uma instância com o SQL Server R Services habilitado. Para esses exemplos, lembre-se de fazer logon usando uma conta que tem a capacidade de criar um novo banco de dados, executar instruções SELECT e exibir tabelas.  Abra uma nova janela **Consulta** e cole esta instrução, apenas para verificar se tudo está funcionando:    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. Criar alguns dados de teste simples  
    
Antes de desenvolver uma solução de ciência de dados complexa, é importante entender as diferenças entre o SQL Server e o R.    
  
1. Crie uma tabela temporária de dados executando a seguinte instrução T-SQL.     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. Assim que a tabela tiver sido criada, use a seguinte instrução para consultar a tabela:  
    ```sql  
    SELECT * from #MyData  
    ```  

**Resultados**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. Obter os dados de teste usando um script do R    
  
Depois que a tabela for criada, execute a seguinte instrução:  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
Ela deve retornar os mesmos valores, mas com um novo nome de coluna.  
  
**Observações**    
- O parâmetro *@language* define a extensão da linguagem a ser chamada, neste caso, o R.    
- No parâmetro *@script*, você define os comandos a serem passados para o tempo de execução do R como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.    
- A linha `N'OutputDataSet <- InputDataSet;'` passa os dados de entrada, contidos no nome da variável padrão **InputDataSet**, para o R e de volta para os resultados sem nenhuma outra operação. Observe que o R diferencia maiúsculas de minúsculas, portanto os nomes das variáveis de entrada e saída devem usar maiúsculas corretamente ou ocorrerá um erro.    
   
    
Para especificar uma variável de entrada ou saída diferente, use o parâmetro *@input_data_1_name* e digite um identificador SQL válido. Por exemplo, neste caso os nomes das variáveis de saída e de entrada foram alterados para *SQLOut* e *SQLIn* respectivamente:    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**Observações**    
- Os parâmetros obrigatórios *@input_data_1* e *@output_data_1* devem ser especificados em primeiro lugar, para que os parâmetros opcionais *@input_data_1_name* e *@output_data_1_name* sejam usados.    
- O SQL e o R não dão suporte aos mesmos tipos de dados. Portanto, geralmente, ocorrem conversões de tipo ao enviar dados do SQL Server para o R e vice-versa. Para obter mais informações, consulte [Trabalhando com tipos de dados do R](../../advanced-analytics/r-services/working-with-r-data-types.md).    
- Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do R e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados.      
- O esquema do conjunto de dados retornado (data.frame do R) é definido pela instrução `WITH RESULT SETS`. Tente omitir isso e veja o que acontece.    
- Os resultados de tabela são retornados no painel **Valores**. As mensagens retornadas pelo tempo de execução do R são fornecidas em **Mensagens**     
  
### 1.4. Gerar resultados usando o R    
    
Você também pode gerar valores usando apenas o script R e deixar a cadeia de caracteres de consulta de entrada em _@input_data_1_ em branco. Ou, você pode usar uma instrução SQL SELECT válida como um espaço reservado, mas não usar os resultados do SQL no script R.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**Resultados**    
    
    
 |*col* |    
 |-----|    
 |*hello*|    
 |     |    
 |*world*|    
    

Agora, tente uma versão diferente do exemplo da Hello World fornecido acima.     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**Resultados**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*hello*|  |*world*|    
    
Observe que as duas instruções criam um vetor com três valores, mas o segundo exemplo retorna três colunas com uma única linha e o primeiro retorna uma única coluna com três linhas. Por quê?
    
Isto acontece porque o R fornece várias maneiras de trabalhar com colunas de valores: vetores, matrizes e listas. Essas operações, embora sejam avançadas e flexíveis, nem sempre atendem às expectativas dos desenvolvedores do SQL.  Algumas funções de R executarão as conversões de objeto de dados implícitos em listas e matrizes.

> [!TIP] 
> 
> Sempre verifique os resultados e determine quantas colunas de dados serão retornadas pelo código do R e quais serão os tipos de dados.    
>     
> Independentemente de seu código R usar matrizes, vetores ou alguma outra estrutura de dados, lembre-se de que o resultado, que é a saída do script R para o procedimento armazenado, deve ser um **data.frame**.      
  
  
## Parte 2 – Conversão de dados e outros problemas  
  
Esta seção fornece uma visão geral de algumas questões a serem consideradas ao executar o código R no SQL Server.  
  
+ Tipos de dados: entender as opções de cast e conversão, bem como conversões implícitas  
+ Conjuntos de resultados de tabela: prever as maneiras pelas quais o R pode alterar colunas e linhas de dados    
  
### 2.1 Coerção implícita de tipos de dados  
    
O R e o SQL Server não usam os mesmos tipos de dados e, portanto, você deve estar ciente das restrições ao mover dados entre o R e o banco de dados. Os exemplos a seguir ilustram esses problemas comuns.   
    
    
1. Execute a seguinte instrução para executar uma multiplicação de matriz usando R.   Nesse script, a única coluna de três valores é convertida em uma matriz de coluna única.  Em seguida, o R converte implicitamente a segunda variável, `y`, em uma matriz de coluna única para adequar os dois argumentos.  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**Resultados**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. Agora, execute o próximo script e veja o que acontece quando você altera o tamanho da matriz. 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**Resultados**    
    
|Col1|
|---|    
|1542|    
  
  Desta vez, o R retorna um único valor como resultado. Esse resultado é válido, porque os dois argumentos são vetores de mesmo tamanho; portanto, o R retornará o produto interno como uma matriz.    
    
   
  
### 2.2 Mesclar ou multiplicar colunas de tamanhos diferentes    
    
  
O script a seguir ilustra alguns comportamentos de R que podem não estar em conformidade com as expectativas de um desenvolvedor de banco de dados.   
  
O script define uma nova matriz numérica de tamanho 6 e a armazena na variável `df1` do R. Em seguida, a matriz numérica é combinada com os inteiros da tabela #MyData, que contém três valores, para criar um novo quadro de dados, `df2`.   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**Resultados**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
Há várias funções do R que criam a saída de tabela, mas que executam operações bem diferentes nos valores, dependendo do objeto de dados do R. Como esse procedimento armazenado do [!INCLUDE[tsql](../../includes/tsql-md.md)] exige que as entradas e saídas sejam passadas como um data.frame, com frequência, você usará funções para converter linhas e colunas de ou em quadros de dados.    
    
Se tiver dúvidas sobre qual objeto de dados do R está sendo usado, adicione a função `str()` do R ou uma das funções de identificação (`is.matrix`, `is.vector`, etc.) para inspecionar os resultados e obter o esquema real e os tipos de valores.    
  
  
Para obter mais informações, consulte este artigo de Hadley Wickham sobre [Estruturas de dados do R](http://adv-r.had.co.nz/Data-structures.html).    
    
### 2.3 Identificar tipos de dados e verificar esquemas   
Você pode ver como é importante saber exatamente quantas colunas serão retornadas pelo código do R e qual será o tipo de dados de cada coluna.     
    
  
Você pode usar a função `str()` no script do R para fazer com que o esquema de dados do objeto do R seja retornado como uma mensagem informativa no . 

Por exemplo, a instrução a seguir retorna o esquema da tabela #MyData.    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**Resultados**    
    
*Mensagens STDOUT do script externo:*    
*'data.frame': 3 obs. de 1 variável:*    
*Mensagens STDOUT do script externo:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 Converter colunas   
  
Quando você envia dados do SQL Server para o R, você precisará com frequência converter os tipos de dados para garantir que possam ser manipulados corretamente.    
  
Quando você usa uma consulta SQL como entrada para o código do R, ocorrem várias transformações dos dados:    
- O SQL Server envia os dados da consulta para o processo do R gerenciado pelo serviço do Launchpad e converte-os em uma representação interna.    
- O tempo de execução do R carrega os dados em uma variável data.frame e executa suas próprias operações nos dados.    
- O mecanismo de banco de dados retorna os dados para o Management Studio ou outro cliente usando tipos de dados do SQL Server.  
    
1. Execute a consulta a seguir no data warehouse AdventureWorksDW. A consulta de dados de entrada define uma tabela de dados de vendas a ser usada na criação de uma previsão.   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. Agora examine os resultados da função `str` para ver como o R tratou os dados de entrada.
      
**Resultados**    
    
  *Mensagem(ns) STDOUT do script externo: 'data.frame':    37 obs. de 3 variáveis:*    
  *Mensagem(ns) STDOUT do script externo: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *Mensagem(ns) STDOUT do script externo: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *Mensagem(ns) STDOUT do script externo: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**Observações**    
    
- Não há suporte para alguns tipos de dados do SQL Server no R. Portanto, para evitar erros, você deve especificar as colunas individualmente e converter algumas delas.    
- O predicado de cadeia de caracteres na cláusula WHERE deve estar entre dois conjuntos de aspas simples.    
- A coluna datetime foi retornada como o tipo de dados do R **POSIXct**.    
- A coluna [ProductSeries] foi identificada (corretamente) como um **fator**.    
     
  
### 2.5 Usar várias entradas   
Apenas um conjunto de dados de entrada pode ser passado como um parâmetro. No entanto, você pode chamar outros conjuntos de dados no código do R, usando RODBC.     
  
Por exemplo, a amostra a seguir faz uma chamada ao pacote RODBC, especificando os dados em uma instrução SELECT.    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

É recomendável que você use o RODBC para obter conjuntos de dados menores, como pesquisas ou listas de fatores e use o parâmetro @input_data para obter conjuntos de dados maiores, como aqueles usados para treinar um modelo, do SQL Server. 


### 2.6 Gerar várias saídas

No SQL Server 2016, a saída do R no procedimento armazenado sp_execute_external_script é limitada a um único data.frame ou conjunto de dados. (Essa limitação poderá ser removida no futuro.)   
No entanto, é possível retornar saídas de outros tipos, além do conjunto de dados. Por exemplo, você poderá treinar um modelo usando um único conjunto de dados como entrada, mas retornar uma tabela de estatísticas como a saída, além do modelo treinado como um objeto.    
    
Além disso, você pode adicionar a palavra-chave `OUTPUT` a qualquer parâmetro de entrada para que ele seja retornado com os resultados.   
    
### 2.7 Processamento paralelo    
    
Se estiver trabalhando com um grande conjunto de dados e a consulta SQL que obtém os dados puder gerar um plano de consulta paralela, você poderá executar um script do R em paralelo, definindo o parâmetro *@parallel* como 1. Em geral, isso será útil se você estiver pontuando um grande conjunto de resultados. Se você usar essa opção, deverá especificar o esquema de resultados de saída com antecedência usando WITH RESULT SETS.    
    
No entanto, esse parâmetro não terá nenhum efeito se você precisar treinar um modelo que usa todas as linhas; nesses casos, recomendamos usar os pacotes **ScaleR**. Esses pacotes podem distribuir o processamento automaticamente sem a necessidade de especificar *@parallel = 1* na chamada a sp_execute_external_script.    
    
      
  
## Parte 3. Como encapsular Funções R em procedimentos armazenados  
  
O R pode realizar várias funções estatísticas avançadas que podem exigir a reprodução de um código complicado usando o T-SQL.  No entanto, com o R Services, você também poderá executar scripts simples do R em um procedimento armazenado para dar suporte a tarefas como estas:   
    
- Aplicar as funções matemáticas e estatísticas do R para dados do SQL Server    
    
- Criar funções com valor de tabela ou funções escalares que usam um código do R    
     

 Normalmente, você deve encapsular as chamadas para essas funções R em procedimentos armazenados, para facilitar a especificação de parâmetros. Para ilustrar esse processo, a mesma função é fornecida no código R, em uma chamada de procedimento armazenado ad hoc para o sp_execute_external_script e em um procedimento armazenado que você pode usar para parametrizar a função R.
 
      
### 3.1. Gerar números aleatórios  
  
A instrução a seguir usa uma das funções do R do pacote `stats`, que é carregado por padrão quando o R Services está instalado. A função `rnorm` mostrada aqui gera 20 números aleatórios com uma distribuição normal, dada uma média de 100.    

Aqui está o código R que faz o trabalho.

```r
as.data.frame(rnorm(20, mean = 100));
```

Essa instrução chama a função do T-SQL e gera os resultados para o SQL Server.  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

Em seguida, você deve encapsular o procedimento armazenado em outro procedimento armazenado para facilitar a especificação de parâmetros. Você deve definir cada um dos parâmetros de entrada no argumento _@params_ e mapear cada parâmetro para o parâmetro R correspondente por nome.

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

Chame o novo procedimento armazenado e especifique os valores.

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2 Mais usos para funções de utilitário do R  
  
Este exemplo chama um dos pacotes de utilitário do R e usa sua função `memory.limit()` para obter memória para o ambiente atual. O pacote `utils` é instalado, mas não é carregado por padrão.    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

O exemplo a seguir obtém o comprimento máximo de números inteiros que têm suporte no computador atual, usando a Função de computador do R e o envia para o console.

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
No entanto, nem sempre o R fará o trabalho melhor. Operações baseadas em conjunto no SQL Server podem ser muito mais eficientes em algumas operações, tanto que cientistas de dados tradicionalmente as executariam no R. Para obter um exemplo de uma comparação de desempenho das funções do R e das funções personalizadas do T-SQL, consulte a [solução Ponta a ponta sobre a Ciência de Dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md). 

Recomendamos avaliar conforme o caso se faz mais sentido executar uma operação específica usando o R, o T-SQL ou alguma outra ferramenta.    
    
    
    
### Recursos adicionais    
    
[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md): esse passo a passo fornece experiência prática em tarefas comuns de ciência de dados    
[Solução de ciência de dados de ponta a ponta](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md): esse passo a passo ilustra um processo de desenvolvimento e implantação que equilibra abordagens do SQL e do R       
[Análise avançada para o Desenvolvedor do SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md): ilustra a operacionalização completa do modelo para o Desenvolvedor do SQL     
    
    
    
    
