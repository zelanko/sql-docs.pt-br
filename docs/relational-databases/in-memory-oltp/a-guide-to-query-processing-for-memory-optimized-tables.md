---
title: Processamento de consulta de tabelas com otimização de memória
ms.custom: seo-dt-2019
ms.date: 05/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 065296fe-6711-4837-965e-252ef6c13a0f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef5c610cb71a0f638c2dfba8aad1fbdb77308dfa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412820"
---
# <a name="a-guide-to-query-processing-for-memory-optimized-tables"></a>Um guia para processamento de consulta de tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O OLTP na memória incorpora as tabelas com otimização de memória e os procedimentos armazenados compilados nativamente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este artigo fornece uma visão geral do processamento de consulta para tabelas com otimização de memória e procedimentos armazenados compilados nativamente.  
  
 O documento explica como as consultas em tabelas com otimização de memória são compiladas e executadas, incluindo:  
  
-   O pipeline do processamento de consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tabelas baseadas em disco.  
  
-   Otimização de consulta; a função de estatísticas sobre tabelas com otimização de memória, bem como diretrizes para solucionar problemas de planos de consulta incorretos.  
  
-   O uso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado para acessar tabelas com otimização de memória.  
  
-   Considerações sobre a otimização de consulta no acesso à tabela com otimização de memória.  
  
-   Compilação e processamento do procedimento armazenado originalmente compilado.  
  
-   Estatísticas que são usadas para estimativa de custo pelo otimizador.  
  
-   Modos de corrigir planos de consulta incorretos.  
  
## <a name="example-query"></a>Consulta de exemplo  
 O exemplo a seguir será usado para ilustrar conceitos de processamento de consulta discutidos neste artigo.  
  
 Vamos considerar duas tabelas, Customer e Order. O script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir contém as definições dessas duas tabelas e os índices associados, em seu formato baseado em disco (tradicional):  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY,  
  ContactName nvarchar (30) NOT NULL   
)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY,  
  CustomerID nchar (5) NOT NULL,  
  OrderDate date NOT NULL  
)  
GO  
CREATE INDEX IX_CustomerID ON dbo.[Order](CustomerID)  
GO  
CREATE INDEX IX_OrderDate ON dbo.[Order](OrderDate)  
GO  
```  
  
 Para construir os planos de consulta mostrados neste artigo, as duas tabelas foram populadas com dados de exemplo do banco de dados de exemplo Northwind, que você pode baixar em [Bancos de dados de exemplo Northwind e pubs do SQL Server 2000](https://www.microsoft.com/download/details.aspx?id=23654).  
  
 Considere a consulta a seguir, que une as tabelas Customer e Order e retorna a ID da ordem e as informações de cliente associadas:  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 O plano de execução estimado, conforme exibido pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é como segue  
  
 ![Plano de consulta para a junção de tabelas com base em disco.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-1.png "Plano de consulta para a junção de tabelas com base em disco.")  
Plano de consulta para a junção de tabelas com base em disco.  
  
 Sobre esse plano de consulta:  
  
-   As linhas da tabela Customer são recuperadas do índice clusterizado, que é a estrutura de dados primária e tem os dados de tabela completos.  
  
-   Os dados da tabela Order são recuperados usando o índice não clusterizado na coluna CustomerID. Esse índice contém a coluna CustomerID, que é usada para a junção, e a coluna de chave primária OrderID, que é retornada ao usuário. O retorno de colunas adicionais da tabela Order exigiria pesquisas no índice clusterizado da tabela Order.  
  
-   O operador lógico **Inner Join** é implementado pelo operador físico **Merge Join**. Os outros tipos de junção física são **Nested Loops** e **Hash Join**. O operador **Merge Join** aproveita o fato de que ambos os índices são classificados na coluna de junção CustomerID.  
  
 Considere uma ligeira variação nessa consulta, que retorna todas as linhas da tabela Order, não apenas OrderID:  
  
```sql  
SELECT o.*, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 O plano estimado para essa consulta é:  
  
 ![Plano de consulta para uma junção hash de tabelas com base em disco.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-2.png "Plano de consulta para uma junção hash de tabelas com base em disco.")  
Plano de consulta para uma junção hash de tabelas com base em disco.  
  
 Nessa consulta, as linhas da tabela Order são recuperadas usando o índice clusterizado. O operador físico **Hash Match** agora é usado para **Inner Join**. O índice clusterizado em Order não é classificado em CustomerID e, portanto, **Merge Join** exigiria um operador de classificação, o que afetaria o desempenho. Observe o custo relativo do operador **Hash Match** (75%) comparado com o custo do operador **Merge Join** no exemplo anterior (46%). O otimizador consideraria o operador **Hash Match** também no exemplo anterior, mas concluiu que o operador **Merge Join** forneceu melhor desempenho.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-query-processing-for-disk-based-tables"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Processamento de consulta para tabelas baseadas em disco  
 O diagrama a seguir descreve o fluxo de processamento de consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para consultas ad hoc:  
  
 ![Pipeline do processamento de consulta do SQL Server.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-3.png "Pipeline do processamento de consulta do SQL Server.")  
Pipeline do processamento de consulta do SQL Server.  
  
 Neste cenário:  
  
1.  O usuário emite uma consulta.  
  
2.  O analisador e o algebrista constroem uma árvore de consulta com operadores lógicos de acordo com o texto [!INCLUDE[tsql](../../includes/tsql-md.md)] enviado pelo usuário.  
  
3.  O otimizador cria um plano de consulta otimizado que contém operadores físicos (por exemplo, junção de loops aninhados). Depois da otimização, o plano pode ser armazenado no cache do plano. Essa etapa será ignorada se o cache do plano já contiver um plano para essa consulta.  
  
4.  O mecanismo de execução de consulta processa uma interpretação do plano de consulta.  
  
5.  Para cada busca de índice, verificação de índice e operador de verificação de tabela, o mecanismo de execução solicita linhas das respectivas estruturas de índice e tabela dos Métodos de Acesso.  
  
6.  Os Métodos de Acesso recuperam as linhas das páginas de dados e de índice no pool de buffers e carregam as páginas do disco no pool de buffers conforme a necessidade.  

 Para a primeira consulta de exemplo, o mecanismo de execução solicita dos Métodos de Acesso as linhas no índice clusterizado em Customer e no índice não clusterizado em Order. Os Métodos de Acesso passam pelas estruturas de índice da árvore B para recuperar as linhas solicitadas. Nesse caso, todas as linhas são recuperadas como os planos de chamada para verificações de índice completo.  
  
## <a name="interpreted-includetsqlincludestsql-mdmd-access-to-memory-optimized-tables"></a>Acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a tabelas com otimização de memória  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc também são conhecidos como [!INCLUDE[tsql](../../includes/tsql-md.md)]. Interpretado se refere ao fato de que o plano de consulta é interpretado pelo mecanismo de execução da consulta para cada operador no plano de consulta. O mecanismo de execução lê o operador e seus parâmetros e executa a operação.  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado pode ser usado para acessar tabelas com otimização de memória e baseadas em disco. A figura a seguir ilustra o processamento de consulta para acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a tabelas com otimização de memória:  
  
 ![Pipeline de processamento da consulta para tsql interpretado.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-4.png "Pipeline de processamento da consulta para tsql interpretado.")  
Pipeline do processamento de consulta para acesso do Transact-SQL interpretado a tabelas com otimização de memória.  
  
 Conforme ilustrado pela figura, na maioria das vezes, o pipeline do processamento de consulta permanece inalterado:  
  
-   O analisador e o algebrista constroem a árvore de consulta.  
  
-   O otimizador cria o plano de execução.  
  
-   O mecanismo de execução de consulta interpresta o plano de execução.  
  
 A principal diferença em relação ao pipeline de processamento de consulta tradicional (figura 2) é que as linhas das tabelas com otimização de memória não são recuperadas no pool de buffers usando os métodos de acesso. Em vez disso, as linhas são recuperadas nas estruturas de dados na memória pelo mecanismo OLTP na memória. As diferenças nas estruturas de dados fazem com que o otimizador escolha planos diferentes em alguns casos, conforme ilustrado pelo exemplo a seguir.  
  
 O script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir contém versões com otimização de memória das tabelas Order e Customer, usando índices de hash:  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY NONCLUSTERED,  
  ContactName nvarchar (30) NOT NULL   
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY NONCLUSTERED,  
  CustomerID nchar (5) NOT NULL INDEX IX_CustomerID HASH(CustomerID) WITH (BUCKET_COUNT=100000),  
  OrderDate date NOT NULL INDEX IX_OrderDate HASH(OrderDate) WITH (BUCKET_COUNT=100000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 Considere a mesma consulta executada em tabelas com otimização de memória:  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 O plano estimado é o seguinte:  
  
 ![Plano de consulta para a junção de tabelas com otimização de memória.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-5.png "Plano de consulta para a junção de tabelas com otimização de memória.")  
Plano de consulta para a junção de tabelas com otimização de memória.  
  
 Observe as seguintes diferenças em relação ao plano para a mesma consulta em tabelas baseadas em disco (figura 1):  
  
-   Esse plano contém uma verificação de tabela em vez de uma verificação de índice clusterizado para a tabela Customer:  
  
    -   A definição da tabela não contém um índice clusterizado.  
  
    -   Os índices clusterizados não têm suporte nas tabelas com otimização de memória. Em vez disso, cada tabela com otimização de memória deve ter pelo menos um índice não clusterizado e todos os índices nas tabelas com otimização de memória podem acessar com eficiência todas as colunas da tabela sem ter que armazená-las no índice ou consultar um índice clusterizado.  
  
-   Esse plano contém **Hash Match** em vez de **Merge Join**. Os índices nas tabelas Order e Customer são índices de hash e, portanto, não são ordenados. Um **Merge Join** exigiria os operadores de classificação que diminuiriam o desempenho.  
  
## <a name="natively-compiled-stored-procedures"></a>procedimentos armazenados compilados nativamente  
 Os procedimentos armazenados compilados nativamente são procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados para código de máquina, não sendo interpretados pela mecanismo de execução de consulta. O script a seguir cria um procedimento armazenado originalmente compilado que executa a consulta de exemplo (na seção Consulta de exemplo).  
  
```sql  
CREATE PROCEDURE usp_SampleJoin  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = 'english')  
  
  SELECT o.OrderID, c.CustomerID, c.ContactName   
FROM dbo.[Order] o INNER JOIN dbo.[Customer] c   
  ON c.CustomerID = o.CustomerID  
  
END  
```  
  
 Os procedimentos armazenados compilados nativamente são compilados no momento da criação, enquanto os procedimentos armazenados interpretados são compilados no momento da primeira execução. (Uma parte da compilação, particularmente de análise e algebrização, ocorre na criação. No entanto, para procedimentos armazenados interpretados, a otimização dos planos de consulta ocorre na primeira execução.) A lógica de recompilação é semelhante. Os procedimentos armazenados compilados nativamente são recompilados na primeira execução do procedimento se o servidor for reiniciado. Os procedimentos armazenados interpretados serão recompilados se o plano não estiver mais no cache do plano. A tabela a seguir resume os casos de compilação e recompilação para procedimentos armazenados interpretados e compilados nativamente:  
  
||Originalmente compilado|Acesso do|  
|-|-----------------------|-----------------|  
|Compilação inicial|No momento da criação.|Na primeira execução.|  
|Recompilação automática|Na primeira execução do procedimento após o reinício do banco de dados ou do servidor.|Na reinicialização do servidor. Ou, remoção do cache do plano, geralmente com base nas alterações de estatísticas ou esquema, ou demanda de memória.|  
|Recompilação manual|Use **sp_recompile**.|Use **sp_recompile**. Você pode remover manualmente o plano do cache, por exemplo, usando DBCC FREEPROCCACHE. Você também pode criar o procedimento armazenado WITH RECOMPILE e o procedimento armazenado será recompilado em cada execução.|  
  
### <a name="compilation-and-query-processing"></a>Processamento de compilação e consulta  
 O diagrama a seguir ilustra o processo de compilação para procedimentos armazenados compilados nativamente:  
  
 ![Compilação original dos procedimentos armazenados.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-6.png "Compilação original dos procedimentos armazenados.")  
Compilação original dos procedimentos armazenados.  
  
 O processo é descrito como:  
  
1.  O usuário emite uma instrução **CREATE PROCEDURE** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  O analisador e o algebrista criam o fluxo de processamento para o procedimento, bem como as árvores de consulta para as consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] no procedimento armazenado.  
  
3.  O otimizador cria planos otimizados de execução de consulta para todas as consultas no procedimento armazenado.  
  
4.  O compilador OLTP na memória usa o fluxo de processamento com os planos de consulta otimizados inseridos e gera uma DLL que contém o código de máquina para execução do procedimento armazenado.  
  
5.  A DLL gerado é carregada na memória.  
  
 A invocação de um procedimento armazenado originalmente compilado é convertida para chamar uma função na DLL.  
  
 ![Execução de procedimentos armazenados compilados nativamente.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-7.png "Execução de procedimentos armazenados compilados nativamente.")  
Execução de procedimentos armazenados compilados nativamente.  
  
 A invocação de um procedimento armazenado originalmente compilado é descrita a seguir:  
  
1.  O usuário emite uma instrução **EXEC**_usp_myproc_ .  
  
2.  O analisador extrai os parâmetros de nome e procedimento armazenado.  
  
     Se a instrução tiver sido preparada, por exemplo, usando **sp_prep_exec**, o analisador não precisará extrair os parâmetros e o nome do procedimento no momento da execução.  
  
3.  O runtime do OLTP na memória localiza o ponto de entrada da DLL do procedimento armazenado.  
  
4.  O código de máquina no DLL é executado e os resultados são retornados para o cliente.  
  
 **Detecção de parâmetro**  
  
 Os procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado são compilados na primeira execução, em oposição aos procedimentos armazenados compilados nativamente, que são compilados no momento da criação. Quando os procedimentos armazenados interpretados são compilados na invocação, os valores dos parâmetros fornecidos para essa invocação são usados pelo otimizador durante a geração do plano de execução. Esse uso de parâmetros durante a compilação é chamado de detecção de parâmetro.  
  
 A detecção de parâmetro não é usada para compilar os procedimentos armazenados compilados nativamente. Todos os parâmetros para o procedimento armazenado são considerados como tendo valores UNKNOWN. Como são procedimentos armazenados interpretados, os procedimentos armazenados compilados nativos também dão suporte à dica de **OPTIMIZE FOR** . Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
### <a name="retrieving-a-query-execution-plan-for-natively-compiled-stored-procedures"></a>Recuperando um plano de execução de consulta para procedimentos armazenados compilados de forma nativa  
 O plano de execução de consulta para um procedimento armazenado compilado nativamente pode ser recuperado usando o **Plano de Execução Estimado** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ou usando a opção SHOWPLAN_XML no [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo:  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC dbo.usp_myproc  
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 O plano de execução gerado pelo otimizador de consulta consiste em uma árvore com operadores de consulta nos nós e nas folhas da árvore. A estrutura da árvore determina a interação (o fluxo de linhas de um operador para outro) entre os operadores. Na exibição gráfica do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o fluxo é da direita para a esquerda. Por exemplo, o plano de consulta na figura 1 contém dois operadores de verificação de índice, que fornece linhas a um operador de junção de mesclagem. O operador de junção de mesclagem fornece linhas a um operador de seleção. O operador de seleção, por fim, retorna as linhas ao cliente.  
  
### <a name="query-operators-in-natively-compiled-stored-procedures"></a>Operadores de consulta nos procedimentos armazenados compilados nativamente  
 A tabela a seguir resume os operadores de consulta com suporte em procedimentos armazenados compilados nativamente:  
  
|Operador|Exemplo de consulta|Observações|  
|--------------|------------------|-----------|  
|SELECT|`SELECT OrderID FROM dbo.[Order]`||  
|INSERT|`INSERT dbo.Customer VALUES ('abc', 'def')`||  
|UPDATE|`UPDATE dbo.Customer SET ContactName='ghi' WHERE CustomerID='abc'`||  
|Delete (excluir)|`DELETE dbo.Customer WHERE CustomerID='abc'`||  
|Compute Scalar|`SELECT OrderID+1 FROM dbo.[Order]`|Esse operador é usado para funções intrínsecas e conversões de tipo. Nem todas as funções e conversões de tipos têm suporte em procedimentos armazenados compilados nativamente.|  
|Nested Loops Join|`SELECT o.OrderID, c.CustomerID FROM dbo.[Order] o INNER JOIN dbo.[Customer] c`|Nested Loops é o único operador de junção com suporte em procedimentos armazenados compilados nativamente. Todos os planos que contêm junções usarão o operador Nested loops, mesmo se o plano para a mesma consulta executada como [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado contiver uma junção de mesclagem ou hash.|  
|Classificar|`SELECT ContactName FROM dbo.Customer ORDER BY ContactName`||  
|TOP|`SELECT TOP 10 ContactName FROM dbo.Customer`||  
|Top-sort|`SELECT TOP 10 ContactName FROM dbo.Customer  ORDER BY ContactName`|A expressão **TOP** (o número de linhas a serem retornadas) não pode exceder 8.000 linhas. Menos se também houver operadores de junção e agregação na consulta. As junções e a agregação normalmente reduzem o número de linhas a serem classificadas, em comparação com a contagem de linhas das tabelas base.|  
|Stream Aggregate|`SELECT count(CustomerID) FROM dbo.Customer`|Observe que o operador Hash Match não tem suporte para agregação. Desse modo, todas as agregações em procedimentos armazenados compilados nativamente usam o operador Stream Aggregate, mesmo se o plano para a mesma consulta no [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado usar o operador Hash Match.|  
  
## <a name="column-statistics-and-joins"></a>Junções e estatísticas de coluna  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém estatísticas sobre valores nas colunas de chave do índice para ajudar a fazer uma estimativa do custo de determinadas operações, como buscas de índice e verificação de índice. (O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também criará estatísticas em colunas de chave não índice se você criá-las explicitamente ou se o otimizador de consulta criá-los em resposta a uma consulta com um predicado.) A principal métrica na estimativa de custo é o número de linhas processadas por um único operador. Observe que para tabelas baseadas em disco, o número de páginas acessadas por um operador específico é significativo na estimativa de custo. No entanto, como a contagem de páginas não é importante para tabelas com otimização de memória (sempre será zero), este documento se concentra na contagem de linhas. A estimativa é iniciada com os operadores de verificação e busca de índice no plano e depois é estendida para incluir os outros operadores, como o de junção. O número estimado de linhas a serem processadas por um operador de junção é baseado na estimativa dos operadores subjacentes de índice, busca e verificação. Para obter acesso do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a tabelas com otimização de memória, você pode observar o plano de execução real ver a diferença entre as contagens de linhas estimadas e reais dos operadores no plano.  
  
 Para o exemplo na figura 1:  
  
-   A verificação de índice clusterizado em Customer estimou 91; real 91.  
  
-   A verificação de índice não clusterizado em CustomerID estimou 830; real 830.  
  
-   O operador Merge Join estimou 815; real 830.  
  
 As estimativas para as verificações de índice são precisas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém a contagem de linhas para tabelas baseadas em disco. As estimativas para verificação de índice e tabela inteira sempre são precisas. A avaliação para a junção é bastante precisa também.  
  
 Se essas estimativas forem alteradas, as considerações de custo para diferentes alternativas de plano também serão alteradas. Por exemplo, se um dos lados da junção tiver uma contagem de linhas estimada de 1 ou apenas algumas linhas, usar as junções de loops aninhados é menos dispendioso.  
  
 Veja a seguir o plano para a consulta;  
  
```  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 Depois de excluir todas as linhas, menos uma na tabela Customer:  
  
 ![Estatísticas e junções de coluna.](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-9.png "Junções e estatísticas de coluna.")  
  
 Em relação a esse plano de consulta:  
  
-   O Hash Match foi substituído por um operador de junção físico Nested Loops.  
  
-   A verificação de índice completo em IX_CustomerID foi substituída por uma busca de índice. Isso resultou na verificação de 5 linhas, em vez das 830 linhas exigidas para a verificação de índice completo.  
  
## <a name="see-also"></a>Consulte Também  
 [Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
