---
title: Criar restrições de verificação | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ace4a96004e22a1c922a491a8f2906c98caefc3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856368"
---
# <a name="create-check-constraints"></a>Criar restrições de verificação
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Você pode criar uma restrição de verificação em uma tabela para especificar quais valores de dados são aceitáveis em uma ou mais colunas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma nova restrição de verificação usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissões ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-new-check-constraint"></a>Para criar uma nova restrição de verificação  
  
1.  No **Pesquisador de Objetos**, expanda a tabela à qual você deseja adicionar uma restrição de verificação, clique com o botão direito do mouse em **Restrições** e clique em **Nova Restrição**.  
  
2.  Na caixa de diálogo **Restrições de Verificação** , clique no campo **Expressão** e clique nas reticências **(…)**.  
  
3.  Na caixa de diálogo **Expressão de Restrição de Verificação** , digite as expressões SQL da restrição de verificação. Por exemplo, para limitar as entradas na coluna `SellEndDate` da tabela `Product` a um valor maior ou igual à data na coluna `SellStartDate` ou a um valor NULL, digite:  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     Ou, para solicitar que as entradas na coluna `zip` sejam de 5 algarismos, digite:  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  Certifique-se de colocar os valores de restrição não numéricos entre aspas simples (').  
  
4.  Clique em **OK**.  
  
5.  Na categoria **Identidade** , você pode alterar o nome da restrição de verificação e adicionar uma descrição (propriedade estendida) para a restrição.  
  
6.  Na categoria **Designer de Tabela** , você pode definir quando a restrição será imposta.  
  
    |**Para:**|**Selecione Sim nos seguintes campos:**|  
    |-------------|---------------------------------------------|  
    |Testar a restrição dos dados que existiam antes da criação da restrição|**Verificar Dados Existentes ao Criar ou Habilitar**|  
    |Impor a restrição sempre que uma operação de replicação ocorrer nesta tabela|**Impor para Replicação**|  
    |Impor a restrição sempre que uma linha desta tabela for inserida ou atualizada|**Impor para INSERTs e UPDATEs**|  
  
7.  Clique em **Fechar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-new-check-constraint"></a>Para criar uma nova restrição de verificação  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
