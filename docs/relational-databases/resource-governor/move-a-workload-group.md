---
title: Mover um grupo de carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: resource-governor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 253478d2c5c26b4a1bc219dc27fe677028959ee0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="move-a-workload-group"></a>Mover um Grupo de Cargas de Trabalho
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode mover um grupo de cargas de trabalho do Administrador de Recursos para um pool de recursos diferente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To move a workload group, using:**  [SQL Server Management Studio](#MoveWGSSMS), [Transact-SQL](#MoveWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Você não pode mover um grupo de cargas de trabalho se houver uma operação de configuração do Administrador de Recursos pendente.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Você não pode mover um grupo de cargas de trabalho se houver uma operação de configuração do Administrador de Recursos pendente. É possível determinar se há uma configuração pendente consultando a exibição de gerenciamento dinâmico de [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) para obter o status atual de is_configuration_pending.  
  
###  <a name="Permissions"></a> Permissões  
 Mover um grupo de cargas de trabalho exige permissão CONTROL SERVER.  
  
##  <a name="MoveWGSSMS"></a> Mover um grupo de cargas de trabalho usando o SQL Server Management Studio  
 **Para mover um grupo de cargas de trabalho usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  No Pesquisador de Objetos, expanda recursivamente o nó **Gerenciamento** para baixo para o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos** e clique em **Propriedades**, para abrir a página **Propriedades do Administrador de Recursos** .  
  
3.  Na janela **Pools de recursos** , clique no pool de recursos que contém o grupo de cargas de trabalho a ser movido. A janela **Grupos de Cargas de Trabalho** agora lista os grupos de cargas de trabalho nesse pool de recursos.  
  
4.  Na janela **Grupos de Cargas de trabalho** , clique com o botão direito do mouse na seta para a direita à esquerda do grupo de cargas de trabalho a ser movido e clique em **Mover para**. Isto exibe uma janela **Mover Grupo de Cargas de Trabalho** .  
  
5.  Os pools de recursos disponíveis são exibidos na janela. Clique no nome do pool de recursos para o qual deseja mover seu grupo de cargas de trabalho e, depois, clique em **OK** para realizar essa ação.  
  
6.  Essa ação só é completada depois de você clicar em **OK**. Ao clicar em **OK**, a instrução ALTER RESOURCE GOVERNOR RECONFIGURE é executada.  
  
7.  Se a operação de criação ou reconfiguração falhar para o pool de recursos ou grupo de cargas de trabalho, um resumo de uma mensagem de erro será exibido abaixo do título da página de propriedades. Para visualizar uma mensagem de erro detalhada, clique na seta para baixo na mensagem de erro.  
  
##  <a name="MoveWGTSQL"></a> Mover grupo de cargas de trabalho usando Transact-SQL  
 **Para mover um grupo de cargas de trabalho usando Transact-SQL**  
  
1.  Execute a instrução **ALTER WORKLOAD GROUP** que especifica o nome do grupo de cargas de trabalho a ser movido e o pool de recursos para o qual ele deve ser movido.  
  
2.  Execute a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir move um grupo de cargas de trabalho chamado `groupAdhoc` para o pool de recursos padrão.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Criar um grupo de carga de trabalho](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
