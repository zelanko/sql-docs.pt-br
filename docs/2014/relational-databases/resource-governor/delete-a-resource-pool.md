---
title: Excluir um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a67b0e2262fa3007597091b6087cc937bb0f3276
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063614"
---
# <a name="delete-a-resource-pool"></a>Excluir um pool de recursos
  É possível excluir um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para excluir um pool de recursos usando:** [SQL Server Management Studio](#DelRPSSMS), [Transact-SQL](#DelRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Não é possível excluir um pool de recursos se ele contiver grupos de cargas de trabalho.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 Você não pode excluir os pools internos ou padrão do Administrador de recursos. Não é possível excluir um pool de recursos se ele contiver grupos de cargas de trabalho. Para obter mais informações, consulte [Delete a Workload Group](delete-a-workload-group.md).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Excluir um pool de recursos exige permissão CONTROL SERVER.  
  
##  <a name="delete-a-resource-pool-using-object-explorer"></a><a name="DelRPSSMS"></a> Excluir um pool de recursos usando o Pesquisador de Objetos  
 **Para excluir um pool de recursos, usando SQL Server Management Studio**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e inclua o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse no pool de recursos a ser excluído e clique em **Excluir**.  
  
3.  Na janela **Excluir Objeto** , o pool de recursos é exibido na lista **Objeto a ser excluído** . Para excluir o pool de recursos, clique em **OK**.  
  
    > [!NOTE]  
    >  Haverá falha ao tentar excluir um pool de recursos que contém um grupo de carga de trabalho.  
  
##  <a name="delete-a-resource-pool-using-transact-sql"></a><a name="DelRPTSQL"></a> Excluir um pool de recursos usando o Transact-SQL  
 **Para excluir um pool de recursos usando o Transact-SQL**  
  
1.  Execute a instrução `DROP RESOURCE POOL` especificando o nome do pool de recursos a ser excluído.  
  
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
 [Administrador de Recursos](resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](resource-governor-resource-pool.md)   
 [Criar um pool de recursos](create-a-resource-pool.md)   
 [Alterar configurações do pool de recursos](change-resource-pool-settings.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
