---
title: Mover um grupo de carga de trabalho | Microsoft Docs
description: Saiba como mover um grupo de carga de trabalho do Resource Governor para um pool de recursos diferente usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a3ff2eff8f72499506aa129b064690693f1b14ff
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86456588"
---
# <a name="move-a-workload-group"></a>Mover um Grupo de Cargas de Trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Você pode mover um grupo de cargas de trabalho do Administrador de Recursos para um pool de recursos diferente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para mover um grupo de cargas de trabalho usando:**  [SQL Server Management Studio](#MoveWGSSMS), [Transact-SQL](#MoveWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Você não pode mover um grupo de cargas de trabalho se houver uma operação de configuração do Administrador de Recursos pendente.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 Você não pode mover um grupo de cargas de trabalho se houver uma operação de configuração do Administrador de Recursos pendente. É possível determinar se há uma configuração pendente consultando a exibição de gerenciamento dinâmico de [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) para obter o status atual de is_configuration_pending.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Mover um grupo de cargas de trabalho exige permissão CONTROL SERVER.  
  
##  <a name="move-a-workload-group-using-sql-server-management-studio"></a><a name="MoveWGSSMS"></a> Mover um grupo de cargas de trabalho usando o SQL Server Management Studio  
 **Para mover um grupo de cargas de trabalho usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  No Pesquisador de Objetos, expanda recursivamente o nó **Gerenciamento** para baixo para o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos** e clique em **Propriedades**, para abrir a página **Propriedades do Administrador de Recursos** .  
  
3.  Na janela **Pools de recursos** , clique no pool de recursos que contém o grupo de cargas de trabalho a ser movido. A janela **Grupos de Cargas de Trabalho** agora lista os grupos de cargas de trabalho nesse pool de recursos.  
  
4.  Na janela **Grupos de Cargas de trabalho** , clique com o botão direito do mouse na seta para a direita à esquerda do grupo de cargas de trabalho a ser movido e clique em **Mover para**. Isto exibe uma janela **Mover Grupo de Cargas de Trabalho** .  
  
5.  Os pools de recursos disponíveis são exibidos na janela. Clique no nome do pool de recursos para o qual deseja mover seu grupo de cargas de trabalho e, depois, clique em **OK** para realizar essa ação.  
  
6.  Essa ação só é completada depois de você clicar em **OK**. Ao clicar em **OK**, a instrução ALTER RESOURCE GOVERNOR RECONFIGURE é executada.  
  
7.  Se a operação de criação ou reconfiguração falhar para o pool de recursos ou grupo de cargas de trabalho, um resumo de uma mensagem de erro será exibido abaixo do título da página de propriedades. Para visualizar uma mensagem de erro detalhada, clique na seta para baixo na mensagem de erro.  
  
##  <a name="move-a-workload-group-using-transact-sql"></a><a name="MoveWGTSQL"></a> Mover grupo de cargas de trabalho usando Transact-SQL  
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
  
  
