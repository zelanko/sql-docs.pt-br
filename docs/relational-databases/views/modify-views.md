---
title: Modificar exibições | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- views [SQL Server], modifying
- modifying views
- renaming views
ms.assetid: 2d3c14dc-43e5-4324-b8fb-f2692d330b16
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d7ef2deee640f5e02908f77f8ad33042ec734814
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40405609"
---
# <a name="modify-views"></a>Modificar exibições
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  Depois de definir uma exibição, é possível alterar sua definição [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sem descartar e recriar a exibição usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar uma exibição usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A modificação de uma exibição não afeta qualquer objeto dependente, como os procedimentos armazenados ou gatilhos; a menos que, a definição da exibição mude de tal maneira que o objeto dependente não seja mais válido.  
  
-   Se uma exibição usada atualmente for modificada com ALTER VIEW, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] obterá um bloqueio de esquema exclusivo na exibição. Quando o bloqueio for concedido e não houver usuários ativos da exibição, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] excluirá todas as cópias da exibição do cache de procedimento. Os planos existentes que façam referência à exibição permanecerão no cache, mas serão recompilados quando invocados.  
  
-   ALTER VIEW pode ser aplicado a exibições indexadas; entretanto, ALTER VIEW descarta incondicionalmente todos os índices da exibição.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar ALTER VIEW, é necessária, no mínimo, permissão ALTER em OBJECT.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-view"></a>Para modificar uma exibição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição ao lado do banco de dados onde sua exibição está localizada e clique no sinal de adição ao lado da pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição a ser modificada e selecione **Design**.  
  
3.  No painel de diagrama do designer de consulta, modifique a exibição de uma ou mais das seguintes formas:  
  
    1.  Marque ou desmarque as caixas de seleção de qualquer elemento que você deseja adicionar ou remover.  
  
    2.  Clique com o botão direito do mouse no painel de diagrama, selecione **Adicionar Tabela…** e selecione as colunas adicionais que deseja incluir na exibição na caixa de diálogo **Adicionar Tabela** .  
  
    3.  Clique com o botão direito do mouse na barra de título da tabela que deseja remover e selecione **Remove**.  
  
4.  No menu **Arquivo**, clique em **Salvar***nome da exibição*.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-a-view"></a>Para modificar uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma exibição primeiro e depois a modifica usando ALTER VIEW. Uma cláusula WHERE é adicionada à definição da exibição.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    -- Create a view.  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
  
    -- Modify the view by adding a WHERE clause to limit the rows returned.  
    ALTER VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID  
    WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;   
    GO  
    ```  
  
 Para obter mais informações, consulte [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md).  
  
  
