---
title: Criar relações de chaves estrangeiras | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 978997ac3048bffb2e8f475d2c728a38b7a27283
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383581"
---
# <a name="create-foreign-key-relationships"></a>Criar relações de chaves estrangeiras
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico descreve como criar relações de chaves estrangeiras no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você cria uma relação entre duas tabelas quando deseja associar linhas de uma tabela com linhas de outra.    
     
##  <a name="BeforeYouBegin"></a> Antes de começar! Limitações e restrições
 
-   Uma restrição de chave estrangeira não precisa estar vinculada apenas a uma restrição de chave primária em outra tabela; ela também pode ser definida para referenciar as colunas de uma restrição UNIQUE em outra tabela.    
    
-   Quando um valor diferente de NULL é inserido na coluna de uma restrição FOREIGN KEY, o valor deve existir na coluna referenciada; caso contrário, será retornada uma mensagem de erro de violação de chave estrangeira. Para garantir que todos os valores de uma restrição FOREIGN KEY composta foram verificados, especifique NOT NULL em todas as colunas participantes.    
    
-   As restrições FOREIGN KEY só podem fazer referência a tabelas que estão no mesmo banco de dados e no mesmo servidor. A integridade referencial em todos os bancos de dados deve ser implementada por gatilhos. Para obter mais informações, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).    
    
-   As restrições FOREIGN KEY podem fazer referência a outra coluna da mesma tabela. Isso se chama autorreferência.    
    
-   Uma restrição FOREIGN KEY especificada no nível da coluna pode listar apenas uma coluna de referência. Essa coluna deve ter o mesmo tipo de dados da coluna na qual a restrição foi definida.    
    
-   Uma restrição FOREIGN KEY especificada no nível da tabela deve ter o mesmo número de colunas de referência da lista de colunas de restrição. O tipo de dados de cada coluna de referência também deve ser igual ao da coluna correspondente na lista de colunas.    
    
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não tem um limite predefinido quanto ao número de restrições FOREIGN KEY que uma tabela pode conter para referenciar outras tabelas nem quanto ao número de restrições FOREIGN KEY que são propriedade de outras tabelas e fazem referência a uma tabela específica. Entretanto, o número real de restrições FOREIGN KEY que pode ser usado é limitado pela configuração do hardware e pelo design do banco de dados e do aplicativo.  Uma tabela pode fazer referência a no máximo 253 outras tabelas e colunas como chaves estrangeiras (referências de saída). [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] aumenta de 253 para 10.000 o limite para o número de outras tabelas e colunas que podem fazer referência a colunas em uma única tabela (referências de entrada).  (Requer, no mínimo, o nível de compatibilidade 130.) O aumento tem as seguintes restrições:    
    
    -   Há suporte para mais de 253 referências de chave estrangeira em operações DELETE and UPDATE DML. Não há suporte para operações MERGE.    
    
    -   Uma tabela com uma referência de chave estrangeira a ela mesma ainda é limitada a 253 referências de chave estrangeira.    
    
    -   O uso de mais de 253 referências de chave estrangeira não está disponível atualmente para índices columnstore, tabelas com otimização de memória nem para o Stretch Database.    
    
-   As restrições FOREIGN KEY não são impostas a tabelas temporárias.    
    
-   Se a chave estrangeira for definida em uma coluna de tipo de dados CLR definido pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).    
    
-   Uma coluna do tipo **varchar(max)** poderá participar de uma restrição FOREIGN KEY somente se a chave primária à qual ela fizer referência também estiver definida como tipo **varchar(max)**.    
    

    
##   <a name="permissions"></a>Permissões    
 A criação de uma nova tabela com uma chave estrangeira requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada.    
    
 Criar uma chave estrangeira em uma tabela existente requer a permissão ALTER na tabela.    
       
    
## <a name="create-a-foreign-key-relationship-in-table-designer"></a>Criar uma relação de chave estrangeira no Designer de Tabela 
####  <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio    
    
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela que estará ao lado da chave estrangeira da relação e clique em **Design**.    
    
     A tabela é aberta no **Designer de Tabela**.    
    
2.  No menu **Designer de Tabela** , clique em **Relações**.    
    
3.  Na caixa de diálogo **Relações de Chave Estrangeira** , clique em **Adicionar**.    
    
     A relação é exibida na lista **Relação Selecionada** com um nome fornecido pelo sistema no formato FK_\<*tablename*>_\<*tablename*>, em que *tablename* é o nome da tabela de chave estrangeira.    
    
4.  Clique na relação na lista **Relação Selecionada** .    
    
5.  Clique em **Especificação de Tabelas e Colunas** na grade à direita e clique nas reticências (**…**) à direita da propriedade.    
    
6.  Na caixa de diálogo **Tabelas e Colunas** , na lista suspensa **Chave Primária** , escolha a tabela que estará ao lado da chave primária da relação.    
    
7.  Na grade inferior, escolha as colunas que contribuem para chave primária da tabela. Na célula da grade adjacente à esquerda de cada coluna, escolha a coluna da chave estrangeira correspondente da tabela da chave estrangeira.    
    
     O**Designer de Tabela** sugere um nome para a relação. Para mudar esse nome, edite o conteúdo da caixa de texto **Nome da Relação** .    
    
8.  Escolha **OK** para criar a relação.    
       
## <a name="create-a-foreign-key-in-a-new-table"></a>Criar uma chave estrangeira em uma nova tabela  
####  <a name="using-transact-sql"></a>Usando Transact-SQL   
    
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].    
    
2.  Na barra Padrão, clique em **Nova Consulta**.    
    
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma tabela e define uma restrição de chave estrangeira na coluna `TempID` que referencia a coluna `SalesReasonID` na tabela `Sales.SalesReason` . As cláusulas ON DELETE CASCADE e ON UPDATE CASCADE são usadas para assegurar a propagação das alterações feitas na tabela `Sales.SalesReason` automaticamente para a tabela `Sales.TempSalesReason` .    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),     
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),     
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    );GO    
    
    ```    
    
## <a name="create-a-foreign-key-in-an-existing-table"></a>Criar uma chave estrangeira em uma tabela existente 
#### <a name="using-transact-sql"></a>Usando Transact-SQL   
    
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].    
    
2.  Na barra Padrão, clique em **Nova Consulta**.    
    
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma chave estrangeira na coluna `TempID` e referencia a coluna `SalesReasonID` na tabela `Sales.SalesReason`.    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    ALTER TABLE Sales.TempSalesReason     
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    ;    
    GO    
    
    ```    
    
     Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md).    
    
  
