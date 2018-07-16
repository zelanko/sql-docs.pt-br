---
title: Criar relações de chaves estrangeiras | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: baf89a41a42a1ea84e37d103890c3c8ea1ed22db
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274552"
---
# <a name="create-foreign-key-relationships"></a>Criar relações de chaves estrangeiras
  Este tópico descreve como criar relações de chaves estrangeiras no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você cria uma relação entre duas tabelas quando deseja associar linhas de uma tabela com linhas de outra.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar relações de chave estrangeira usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Uma restrição de chave estrangeira não precisa estar vinculada apenas a uma restrição de chave primária em outra tabela; ela também pode ser definida para referenciar as colunas de uma restrição UNIQUE em outra tabela.  
  
-   Quando um valor diferente de NULL é inserido na coluna de uma restrição FOREIGN KEY, o valor deve existir na coluna referenciada; caso contrário, será retornada uma mensagem de erro de violação de chave estrangeira. Para garantir que todos os valores de uma restrição FOREIGN KEY composta foram verificados, especifique NOT NULL em todas as colunas participantes.  
  
-   As restrições FOREIGN KEY só podem fazer referência a tabelas que estão no mesmo banco de dados e no mesmo servidor. A integridade referencial em todos os bancos de dados deve ser implementada por gatilhos. Para obter mais informações, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
-   As restrições FOREIGN KEY podem fazer referência a outra coluna da mesma tabela. Isso se chama autorreferência.  
  
-   Uma restrição FOREIGN KEY especificada no nível da coluna pode listar apenas uma coluna de referência. Essa coluna deve ter o mesmo tipo de dados da coluna na qual a restrição foi definida.  
  
-   Uma restrição FOREIGN KEY especificada no nível da tabela deve ter o mesmo número de colunas de referência da lista de colunas de restrição. O tipo de dados de cada coluna de referência também deve ser igual ao da coluna correspondente na lista de colunas.  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não tem um limite predefinido quanto ao número de restrições FOREIGN KEY que uma tabela pode conter para referenciar outras tabelas nem quanto ao número de restrições FOREIGN KEY que são propriedade de outras tabelas e fazem referência a uma tabela específica. Entretanto, o número real de restrições FOREIGN KEY que pode ser usado é limitado pela configuração do hardware e pelo design do banco de dados e do aplicativo. Recomendamos que uma tabela não contenha mais de 253 restrições FOREIGN KEY e que ela não seja referenciada por mais de 253 restrições FOREIGN KEY.  
  
-   As restrições FOREIGN KEY não são impostas a tabelas temporárias.  
  
-   Se a chave estrangeira for definida em uma coluna de tipo de dados CLR definido pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
-   A coluna do tipo `varchar(max)` poderá participar de uma restrição FOREIGN KEY somente se a chave primária que ela referencia também estiver definida como tipo `varchar(max)`.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A criação de uma nova tabela com uma chave estrangeira requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada.  
  
 Criar uma chave estrangeira em uma tabela existente requer a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-foreign-key-relationship-in-table-designer"></a>Para criar uma relação de chave estrangeira no Designer de Tabela  
  
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
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-foreign-key-in-a-new-table"></a>Para criar uma chave estrangeira em uma nova tabela  
  
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
  
#### <a name="to-create-a-foreign-key-in-an-existing-table"></a>Para criar uma chave estrangeira em uma tabela existente  
  
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
  
     Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql), [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) e [table_constraint &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql).  
  
  
