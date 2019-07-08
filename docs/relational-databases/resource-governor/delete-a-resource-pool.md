---
title: Excluir um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: c389ed72d7aa6f49c320585ee8f23e35eaec1bc7
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581815"
---
# <a name="delete-a-resource-pool"></a>Excluir um pool de recursos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  É possível excluir um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para excluir um pool de recursos usando:** [SQL Server Management Studio](#DelRPSSMS), [Transact-SQL](#DelRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Não é possível excluir um pool de recursos se ele contiver grupos de cargas de trabalho.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Você não pode excluir os pools internos ou padrão do Administrador de recursos. Não é possível excluir um pool de recursos se ele contiver grupos de cargas de trabalho. Para obter mais informações, consulte [Delete a Workload Group](../../relational-databases/resource-governor/delete-a-workload-group.md).  
  
###  <a name="Permissions"></a> Permissões  
 Excluir um pool de recursos exige permissão CONTROL SERVER.  
  
##  <a name="DelRPSSMS"></a> Excluir um pool de recursos usando o Pesquisador de Objetos  
 **Para excluir um pool de recursos, usando SQL Server Management Studio**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e inclua o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse no pool de recursos a ser excluído e clique em **Excluir**.  
  
3.  Na janela **Excluir Objeto** , o pool de recursos é exibido na lista **Objeto a ser excluído** . Para excluir o pool de recursos, clique em **OK**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    > [!NOTE]  
    >  If the resource pool that you are trying to delete contains a workload group, this action will fail.  
  
##  <a name="DelRPTSQL"></a> Excluir um pool de recursos usando o Transact-SQL  
 **Para excluir um pool de recursos usando o Transact-SQL**  
  
1.  Execute a instrução **DROP RESOURCE POOL** ou **DROP EXTERNAL RESOURCE POOL** especificando o nome do pool de recursos a ser excluído.  
  
2.  Execute a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O seguinte exemplo descarta um grupo de carga de trabalho denominado `poolAdhoc`.  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
