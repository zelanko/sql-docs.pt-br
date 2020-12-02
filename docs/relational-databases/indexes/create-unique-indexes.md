---
description: Criar índices exclusivos
title: Criar índices exclusivos | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- unique indexes
- designing indexes [SQL Server], unique
- clustered indexes, unique
- indexes [SQL Server], unique
- nonclustered indexes [SQL Server], unique
- unique indexes, design guidelines
ms.assetid: 56b5982e-cb94-46c0-8fbb-772fc275354a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 59ab82f18d59bd6a2f8df0c236cd44031b740ee1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130257"
---
# <a name="create-unique-indexes"></a>Criar índices exclusivos
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico descreve como criar um índice exclusivo em uma tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um índice exclusivo garante que a chave de índice não contém nenhum valor duplicado e, portanto, cada linha na tabela é exclusiva de algum modo. Não existe nenhuma diferença significativa entre criar uma restrição UNIQUE e criar um índice exclusivo que seja independente de uma restrição. A validação de dados ocorre da mesma maneira, e o otimizador de consultas não diferencia entre um índice exclusivo criado por uma restrição ou manualmente criado. No entanto, criar uma restrição UNIQUE na coluna torna claro o objetivo do índice. Para obter mais informações sobre restrições UNIQUE, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 Quando você criar um índice exclusivo, será possível definir uma opção para ignorar chaves duplicadas. Se essa opção for definida como **Sim** e você tentar criar chaves duplicadas adicionando dados que afetem várias linhas (com a instrução INSERT), a linha que contém uma duplicata não será adicionada. Se ela for definida como **Não**, ocorrerá falha em toda a operação de inserção e todos os dados serão revertidos.  
  
> [!NOTE]  
>  Você não poderá criar um índice exclusivo em uma única coluna se ela tiver NULL em mais de uma linha. Da mesma forma, você não poderá criar um índice exclusivo em várias colunas se a combinação de colunas tiver NULL em mais de uma linha. Isso é tratado como valores duplicados para fins de indexação.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Benefícios de um índice exclusivo](#Benefits)  
  
     [Implementações comuns](#Implementations)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um índice exclusivo em uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="benefits-of-a-unique-index"></a><a name="Benefits"></a> Benefícios de um índice exclusivo  
  
-   Índices exclusivos de multicolunas garantem que cada combinação de valores na chave de índice é exclusivo. Por exemplo, se um índice exclusivo for criado em uma combinação de colunas **LastName**, **FirstName** e **MiddleName** , duas linhas na tabela não poderão ter a mesma combinação de valores que essas colunas.  
  
-   Contanto que os dados em cada coluna sejam exclusivos, você pode criar um índice clusterizado exclusivo e vários índices exclusivos não clusterizados na mesma tabela.  
  
-   Os índices exclusivos garantem a integridade de dados das colunas definidas.  
  
-   Índices exclusivos fornecem informações adicionais úteis para o otimizador de consulta que pode gerar planos de execução mais eficientes.  
  
###  <a name="typical-implementations"></a><a name="Implementations"></a> Implementações comuns  
 Os índices exclusivos são implementados das seguintes maneiras:  
  
-   **Restrição PRIMARY KEY ou UNIQUE**  
  
     Quando se cria uma restrição PRIMARY KEY, é criado automaticamente um índice clusterizado exclusivo na coluna ou a coluna é automaticamente criada se não existir um índice clusterizado na tabela e você não especificar um índice não clusterizado exclusivo. A coluna de chave primária não pode permitir valores NULL.  
  
     Quando se cria uma restrição UNIQUE, é criado, por padrão, um índice não clusterizado exclusivo para impor uma restrição UNIQUE por padrão. Você pode especificar um índice clusterizado exclusivo caso ainda não exista um índice clusterizado na tabela.  
  
     Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) e [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md).  
  
-   **Índice independente de uma restrição**  
  
     Vários índices não clusterizado exclusivos podem ser definidos em uma tabela.  
  
     Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
-   **Exibição indexada**  
  
     Para criar uma exibição indexada, um índice clusterizado exclusivo é definido em uma ou mais colunas de exibição. A exibição é executada e o conjunto de resultados é armazenado no nível folha do índice da mesma forma que os dados de tabela são armazenados em um índice clusterizado. Para obter mais informações, veja [Criar exibições indexadas](../../relational-databases/views/create-indexed-views.md).  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Um índice exclusivo, uma restrição UNIQUE ou uma restrição PRIMARY KEY não poderão ser criados, se existirem valores de chave duplicados nos dados.  
  
-   Um índice não clusterizado exclusivo pode conter colunas não chave incluídas. Para obter mais informações, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-unique-index-by-using-the-table-designer"></a>Para criar um índice exclusivo usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja criar um índice exclusivo.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela na qual você deseja criar um índice exclusivo e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , selecione **Índices/Chaves**.  
  
5.  Na caixa de diálogo **Índices/Chaves** , clique em **Adicionar**.  
  
6.  Selecione o novo índice na caixa de texto **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
7.  Na grade principal, em **(Geral)** , selecione **Tipo** e escolha **Índice** na lista.  
  
8.  Selecione **Colunas** e clique no botão reticências **(...)** .  
  
9. Na caixa de diálogo **Colunas de Índice** , em **Nome da Coluna**, selecione as colunas que você deseja indexar. Você pode selecionar até 16 colunas. Para um desempenho ideal, selecione somente uma ou duas colunas por índice. Para cada coluna selecionada, indique se o índice organiza os valores dessa coluna em ordem crescente ou decrescente.  
  
10. Quando todas as colunas para o índice estiverem selecionadas, clique em **OK**.  
  
11. Na grade, em **(Geral)** , selecione **É Exclusivo** e escolha **Sim** na lista.  
  
12. Opcional: na grade principal, em **Designer de Tabela**, selecione **Ignorar Chaves Duplicadas** e escolha **Sim** na lista. Faça isso se você desejar ignorar as tentativas de adição de dados que criariam uma chave duplicada no índice exclusivo.  
  
13. Clique em **fechar**  
  
14. No menu **Arquivo**, clique em **Salvar**_table\_name_.  
  
#### <a name="create-a-unique-index-by-using-object-explorer"></a>Crie um índice exclusivo usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja criar um índice exclusivo.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja criar um índice exclusivo.  
  
4.  Clique com o botão direito do mouse na pasta **Índices**, aponte para **Novo Índice** e selecione **Índice Não Clusterizado...** .  
  
5.  Na caixa de diálogo **Novo Índice** , na página **Geral** , insira o nome do novo índice na caixa **Nome do índice** .  
  
6.  Marque a caixa de seleção **Exclusivo** .  
  
7.  Em **Colunas de chave de índice**, clique em **Adicionar...** .  
  
8.  Na caixa de diálogo **Selecionar Colunas de**_table\_name_, marque as caixas de seleção das colunas da tabela ou das colunas a serem adicionadas ao índice exclusivo.  
  
9. Clique em **OK**.  
  
10. Na caixa de diálogo **Novo Índice** , clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-unique-index-on-a-table"></a>Para criar um índice exclusivo em uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named AK_UnitMeasure_Name and delete it if found  
    IF EXISTS (SELECT name from sys.indexes  
               WHERE name = N'AK_UnitMeasure_Name')   
       DROP INDEX AK_UnitMeasure_Name ON Production.UnitMeasure;   
    GO  
    -- Create a unique index called AK_UnitMeasure_Name  
    -- on the Production.UnitMeasure table using the Name column.  
    CREATE UNIQUE INDEX AK_UnitMeasure_Name   
       ON Production.UnitMeasure (Name);   
    GO  
    ```  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  
