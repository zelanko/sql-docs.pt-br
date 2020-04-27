---
title: Criar um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4d18ef352c3e5ab6342e573d16bc3deaed5db72
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211996"
---
# <a name="create-a-resource-pool"></a>Criar um pool de recursos
  É possível criar um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **Para criar um pool de recursos, usando:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 O percentual máximo de CPU deve ser igual a ou maior que o percentual mínimo de CPU. O percentual máximo de memória deve ser igual a ou maior que o percentual mínimo de memória.  
  
 A soma dos percentuais mínimos de CPU e dos percentuais mínimos de memória de todos os pools de recursos não deve exceder 100.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Criar um pool de recursos exige permissão CONTROL SERVER.  
  
##  <a name="create-a-resource-pool-using-sql-server-management-studio"></a><a name="CreRPProp"></a> Criar um pool de recursos usando o SQL Server Management Studio  
 **Para criar um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e inclua o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Resource Governor**e então clique em **Propriedades**.  
  
3.  Na grade **Pools de recursos** , clique na primeira coluna na linha vazia. Essa coluna está rotulada com um asterisco (*).  
  
4.  Clique duas vezes na célula vazia na coluna **Nome** . Digite o nome que você quer usar para o pool de recursos.  
  
5.  Clique ou clique duas vezes em outras células na linha que você quer alterar e insira os novos valores.  
  
6.  Para salvar as alterações, clique em **OK**  
  
##  <a name="create-a-resource-pool-using-transact-sql"></a><a name="CreRPTSQL"></a>Criar um pool de recursos usando o Transact-SQL  
 **Para criar um pool de recursos usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Execute a instrução `CREATE RESOURCE POOL` especificando os valores de propriedade a serem definidos.  
  
2.  Execute a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir cria um pool de recursos denominado `poolAdhoc`.  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Resource Governor](resource-governor.md)   
 [Habilitar Resource Governor](enable-resource-governor.md)   
 [Resource Governor pool de recursos](resource-governor-resource-pool.md)   
 [Alterar configurações do pool de recursos](change-resource-pool-settings.md)   
 [Excluir um pool de recursos](delete-a-resource-pool.md)   
 [Configurar Resource Governor usando um modelo](configure-resource-governor-using-a-template.md)   
 [Grupo de carga de trabalho Resource Governor](resource-governor-workload-group.md)   
 [Resource Governor função de classificação](resource-governor-classifier-function.md)   
 [CRIAR POOL de recursos &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
