---
title: Criar tabelas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table creation [SQL Server], Visual Database Tools
ms.assetid: 6f7c6ac5-e6d3-4dca-831e-b28442ba535b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 261aab8b0e8a5d80aed143d6b29e952243742917
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176806"
---
# <a name="create-tables-database-engine"></a>Criar tabelas (Mecanismo de Banco de Dados)
  Você pode criar uma nova tabela, nomeá-la e adicioná-la a um banco de dados existente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
>  Se você estiver conectado a um banco de dados SQL Azure, a nova opção de tabela iniciará um script de modelo de criação de tabela. Edite os parâmetros e execute o script para criar uma nova tabela. Para obter mais informações, consulte [SQL Azure Overview](https://microsoft.sharepoint.com/sites/infopedia_g01/pages/cards/azure-sql-database.aspx)(em inglês).

 **Neste tópico**

-   **Antes de começar:**

     [Segurança](#Security)

-   **Para criar uma tabela usando:**

     [SQL Server Management Studio](#SSMSProcedure)

     [Transact-SQL](#TsqlProcedure)

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

###  <a name="security"></a><a name="Security"></a> Segurança

####  <a name="permissions"></a><a name="Permissions"></a> Permissões
 Requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada.

 Se alguma coluna da instrução CREATE TABLE for definida como um tipo de dados CLR definido pelo usuário, a propriedade do tipo ou a permissão REFERENCES será necessária.

 Se alguma coluna da instrução CREATE TABLE tiver uma coleção de esquemas XML associada a ela, a propriedade da coleção de esquemas XML ou a permissão REFERENCES é necessária.

##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

#### <a name="to-create-a-table-with-table-designer"></a>Para criar uma tabela com o Designer de Tabela

1.  No **Pesquisador de Objetos**, conecte-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que contém o banco de dados a ser modificado.

2.  No **Pesquisador de Objetos**, expanda o nó **Bancos de Dados** e, em seguida, expanda o banco de dados que conterá a nova tabela.

3.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó **Tabelas** do banco de dados e clique em **Nova Tabela**.

4.  Digite nomes de coluna, escolha tipos de dados e opte por permitir ou não nulos para cada coluna, conforme ilustrado a seguir.

     ![AddColumnsinTableDesigner](../../database-engine/media/addcolumnsintabledesigner.gif "AddColumnsinTableDesigner")

5.  Para especificar mais propriedades para uma coluna, como valores de identidade ou de coluna computada, clique na coluna e na guia propriedades de coluna, escolha as propriedades adequadas. Para obter mais informações sobre as propriedades de coluna, veja [Propriedades de coluna da tabela &#40;SQL Server Management Studio&#41;](table-column-properties-sql-server-management-studio.md).

6.  Para especificar uma coluna como chave primária, clique com o botão direito do mouse na coluna e selecione **Definir Chave Primária**. Para obter mais informações, consulte [Create Primary Keys](../tables/create-primary-keys.md).

7.  Para criar relações de chave estrangeira, restrições de verificação ou índices, clique com o botão direito do mouse no painel Designer de Tabela e selecione um objeto da lista, conforme mostrado na ilustração a seguir.

     ![AddTableObjects](../../database-engine/media/addtableobjects.gif "AddTableObjects")

     Para obter mais informações sobre esses objetos, consulte [Create Foreign Key Relationships](../tables/create-foreign-key-relationships.md), [Create Check Constraints](../tables/create-check-constraints.md) e [Indexes](../indexes/indexes.md).

8.  Por padrão, a tabela está contida no esquema **dbo** . Para especificar um esquema diferente para a tabela, clique com o botão direito do mouse no painel Designer de Tabela e selecione **Propriedades** , conforme ilustrado a seguir. Na lista suspensa **Esquema** , selecione o esquema apropriado.

     ![Specifyatableschema](../../database-engine/media/specifyatableschema.gif "Specifyatableschema")

     Para obter mais informações sobre esquemas, consulte [Create a Database Schema](../security/authentication-access/create-a-database-schema.md).

9. No menu **Arquivo**, escolha **Salvar** *nome da tabela*.

10. Na caixa de diálogo **Escolher Nome** , digite um nome para a tabela e clique em **OK**.

11. Para exibir a nova tabela, em **Pesquisador de Objetos**, expanda o nó **Tabelas** e pressione **F5** para atualizar a lista de objetos. A nova tabela é exibida na lista de tabelas.

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

#### <a name="to-create-a-table-in-the-query-editor"></a>Para criar uma tabela no Editor de Consultas

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2.  Na barra Padrão, clique em **Nova Consulta**.

3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.

    ```
    CREATE TABLE dbo.PurchaseOrderDetail
    (
        PurchaseOrderID int NOT NULL
        ,LineNumber smallint NOT NULL
        ,ProductID int NULL
        ,UnitPrice money NULL
        ,OrderQty smallint NULL
        ,ReceivedQty float NULL
        ,RejectedQty float NULL
        ,DueDate datetime NULL
    );
    ```

 Para obter mais exemplos, veja [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).


