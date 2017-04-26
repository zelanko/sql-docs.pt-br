---
title: "Criar índices filtrados | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de8d5ce869856d289b70b028ede2bc1009220a38
ms.lasthandoff: 04/11/2017

---
# <a name="create-filtered-indexes"></a>Criar índices filtrados
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico descreve como criar um índice filtrado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um índice filtrado é um índice não clusterizado otimizado, criado especialmente para consultas que fazem seleções a partir de um subconjunto bem definido de dados. Ele usa um predicado de filtro para indexar uma parte das linhas da tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta, bem como reduzir os custos de manutenção e de armazenamento do índice em comparação com os índices de tabela completa.  
  
 Os índices filtrados podem oferecer as seguintes vantagens com relação aos índices de tabela completa:  
  
-   **Melhor desempenho de consultas e qualidade de plano**  
  
     Um índice filtrado bem projetado melhora o desempenho das consultas e a qualidade do plano de execução porque é menor do que um índice não clusterizado de tabela completa e possui estatísticas filtradas. As estatísticas filtradas são mais precisas do que as estatísticas de tabela completa, pois abrangem apenas as linhas do índice filtrado.  
  
-   **Redução dos custos de manutenção do índice**  
  
     A manutenção do índice é feita apenas quando as instruções DML (linguagem de manipulação de dados) afetam os dados do índice. Um índice filtrado reduz os custos de manutenção em comparação com o índice não clusterizado de tabela completa porque é menor e a manutenção é feita somente quando seus dados são alterados. É possível ter um grande número de índices filtrados, especialmente quando eles contêm dados que são raramente alterados. Do mesmo modo, se um índice filtrado tiver apenas dados modificados com frequência, seu tamanho reduzido diminuirá o custo de atualização das estatísticas.  
  
-   **Redução dos custos de armazenamento do índice**  
  
     A criação de um índice filtrado pode reduzir o armazenamento em disco de índices não clusterizados quando um índice de tabela completa não é necessário. É possível substituir um índice não clusterizado de tabela completa por vários índices filtrados sem aumentar de forma significativa os requisitos de armazenamento.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Considerações de criação](#Design)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um índice filtrado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Design"></a> Considerações de criação  
  
-   Quando a coluna tem apenas uma pequena quantidade de valores relevantes para consultas, você pode criar um índice filtrado no subconjunto de valores. Por exemplo, se os valores de uma coluna forem predominantemente NULL e a consulta selecionar apenas valores não NULL, será possível criar um índice filtrado para linhas de dados não NULL. O índice resultante será menor e sua manutenção será menos dispendiosa em comparação com um índice não clusterizado de tabela completa definido nas mesmas colunas de chave.  
  
-   Quando a tabela contém linhas de dados heterogêneos, é possível criar um índice filtrado para uma ou mais categorias de dados. Isso pode melhorar o desempenho das consultas nessas linhas de dados limitando o foco de uma consulta a uma área específica da tabela. Novamente, o índice resultante será menor e sua manutenção será menos dispendiosa em comparação com um índice não clusterizado de tabela completa.  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Não é possível criar um índice filtrado em uma exibição. No entanto, o otimizador de consulta pode se beneficiar do índice filtrado definido em uma tabela referenciada em uma exibição. O otimizador de consulta considera um índice filtrado para uma consulta que seleciona uma exibição se os resultados da consulta estiverem corretos.  
  
-   Os índices filtrados têm as seguintes vantagens em relação às exibições indexadas:  
  
    -   Redução dos custos de manutenção do índice. Por exemplo, o processador de consulta usa menos recursos da CPU para atualizar um índice filtrado do que uma exibição indexada.  
  
    -   Melhor qualidade de plano. Por exemplo, durante a compilação de uma consulta, o otimizador de consulta considera usar um índice filtrado em mais situações do que a exibição indexada equivalente.  
  
    -   Recriações de índice online. É possível recriar índices filtrados enquanto estão disponíveis para consultas. As recriações de índices online não têm suporte para exibições indexadas. Para obter mais informações, veja a opção REBUILD de [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
    -   Índices não exclusivos. Os índices filtrados podem ser não exclusivos, enquanto as exibições indexadas devem ser exclusivas.  
  
-   Os índices filtrados são definidos em uma tabela e oferecem suporte apenas a operadores de comparação simples. Se você precisar de uma expressão de filtro que referencie várias tabelas ou que tenha uma lógica complexa, deverá criar uma exibição.  
  
-   A coluna na expressão do índice filtrado não precisará ser uma coluna de chave ou incluída na definição do índice filtrado, se a expressão do índice filtrado for equivalente ao predicado da consulta e a consulta não retorná-la com os resultados da consulta.  
  
-   A coluna na expressão de índice filtrado deverá ser uma coluna de chave ou incluída na definição do índice filtrado se o predicado de consulta usá-la em uma comparação que não for equivalente à expressão do índice filtrado.  
  
-   A coluna na expressão do índice filtrado deverá ser uma coluna de chave ou incluída na definição do índice filtrado se fizer parte do conjunto de resultados da consulta.  
  
-   A chave de índice clusterizado da tabela não precisa ser uma coluna de chave ou incluída na definição do índice filtrado. A chave de índice clusterizado é incluída automaticamente em todos os índices não clusterizados, inclusive índices filtrados.  
  
-   Se o operador de comparação especificado na expressão do índice filtrado resultar em uma conversão de dados implícita ou explícita, ocorrerá um erro se a conversão ocorrer à esquerda do operador de comparação. Uma solução seria gravar a expressão do índice filtrado com o operador de conversão de dados (CAST ou CONVERT) à direita do operador de comparação.  

- Examine as opções SET necessárias para a criação de índice filtrado na sintaxe [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** . Para modificar a expressão de índice filtrado, use CREATE INDEX WITH DROP_EXISTING.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-filtered-index"></a>Para criar um índice filtrado  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja criar um índice filtrado.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição ao lado da tabela na qual você deseja criar um índice filtrado.  
  
4.  Clique com o botão direito do mouse na pasta **Índices** , aponte para **Novo Índice**e selecione **Índice Não Clusterizado…**.  
  
5.  Na caixa de diálogo **Novo Índice** , na página **Geral** , insira o nome do novo índice na caixa **Nome do índice** .  
  
6.  Na guia **Colunas de chave de índice**, clique em **Adicionar…**.  
  
7.  Na caixa de diálogo **Selecionar Colunas de***table_name* , marque as caixas de seleção das colunas da tabela a serem adicionadas ao índice exclusivo.  
  
8.  Clique em **OK**.  
  
9. Na página **Filtro** , em **Expressão de Filtro**, digite a expressão SQL que você usará para criar o índice filtrado.  
  
10. Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-create-a-filtered-index"></a>Para criar um índice filtrado  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     O índice filtrado acima é válido para a consulta a seguir. Você pode exibir o plano de execução da consulta para determinar se o otimizador de consulta usou o índice filtrado.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>Para garantir que um índice filtrado seja usado em uma consulta SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  

