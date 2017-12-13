---
title: Desabilitar Resource Governor | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: resource-governor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69ff08716168f02736aa5a4ce8eb340fba637bc0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="disable-resource-governor"></a>Desabilitar Administrador de Recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Você pode desabilitar o Resource Governor usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Antes de começar:**  [Limitações e restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para desabilitar o Administrador de Recursos, usando:**  [Pesquisador de Objetos](#RGOffObjEx), [Propriedades do Administrador de Recursos](#RGOffProp), [Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 A desabilitação do Administrador de Recursos gera os seguintes resultados:  
  
-   A função de classificação não é executada.  
  
-   Todas as conexões novas são automaticamente classificadas no grupo de cargas de trabalho padrão.  
  
-   As solicitações iniciadas pelo sistema são classificadas no grupo de cargas de trabalho interno.  
  
-   Todas as configurações existentes do grupo de carga de trabalho e do pool de recursos são redefinidas para os valores padrão. Nesse caso, nenhum evento é acionado quando os limites são atingidos.  
  
-   O monitoramento normal do sistema não é afetado.  
  
-   As alterações de configuração podem ser feitas, mas as alterações não entram em vigor até que o Administrador de Recursos seja habilitado.  
  
-   Depois que o SQL Server for reiniciado, o Administrador de Recursos não carregará sua configuração, mas em vez disso terá apenas os grupos de cargas de trabalho e pools de recursos padrão e internos.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Você não pode usar a instrução **ALTER RESOURCE GOVERNOR** para desabilitar o Administrador de Recursos durante uma transação de usuário.  
  
###  <a name="Permissions"></a> Permissões  
 Desabilitar o Administrador de Recursos exige permissão CONTROL SERVER.  
  
##  <a name="RGOffObjEx"></a> Desabilitar o Administrador de Recursos usando o Pesquisador de Objetos  
 **Para desabilitar o Administrador de Recursos usando o Pesquisador de Objetos**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e incluindo o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos**e, então, clique em **Desabilitar**.  
  
##  <a name="RGOffProp"></a> Desabilitar o Administrador de Recursos usando as Propriedades do Administrador de Recursos  
 **Para desabilitar o Administrador de Recursos usando a página de propriedades do Administrador de Recursos**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e incluindo o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos** e clique em **Propriedades**, para abrir a página **Propriedades do Administrador de Recursos** .  
  
3.  Clique na caixa de seleção **Habilitar Administrador de Recursos** , verifique se a caixa não está selecionada e clique em **OK**.  
  
##  <a name="RGOffTSQL"></a> Desabilitar o Administrador de Recursos usando Transact-SQL  
 **Para desabilitar o Administrador de Recursos usando Transact-SQL**  
  
1.  Execute a instrução **ALTER RESOURCE GOVERNOR DISABLE** .  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir habilita o Administrador de Recursos.  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
