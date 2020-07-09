---
title: Criar um pool de recursos | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 4ddcb42d6a91eab41cddf3beb53c0de6a6b25d36
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720539"
---
# <a name="create-a-resource-pool"></a>Criar um pool de recursos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  É possível criar um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para entender os princípios de pools de recursos, consulte [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para criar um pool de recursos usando:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
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
  
##  <a name="create-a-resource-pool-using-transact-sql"></a><a name="CreRPTSQL"></a> Criar um pool de recursos usando o Transact-SQL  
 **Para criar um pool de recursos usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Execute a instrução [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) ou [CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) que especifica os valores de propriedade a serem definidos.  
  
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
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Excluir um pool de recursos](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Configurar o administrador de recursos usando um modelo](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
