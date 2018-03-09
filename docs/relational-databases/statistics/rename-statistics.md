---
title: "Renomear estatísticas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: statistics
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming statistics
- statistics [SQL Server], renaming
ms.assetid: a3bed7b7-3dc5-4b33-b1c6-67c27f573764
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4fa52b31a89efdd5473012ca5f17a20f5b3eed8
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="rename-statistics"></a>Renomear estatísticas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode renomear um objeto de estatísticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear um objeto de estatísticas, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Por padrão, a criação de um índice cria uma estatística nas colunas de chave desse índice. Portanto, a renomeação do índice renomeia automaticamente o objeto de estatísticas e vice-versa.  
  
 A alteração de qualquer parte de um nome de objeto pode quebrar scripts e procedimentos armazenados. Em vez de renomear, é recomendável que você remova o objeto de estatísticas e recrie-o com o novo nome.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-rename-a-statistics-object"></a>Para renomear um objeto de estatísticas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename N'AK_Employee_LoginID', N'AK_Emp_Login', N'STATISTICS';   
    GO  
    ```  
  
 Para obter mais informações, veja [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  
