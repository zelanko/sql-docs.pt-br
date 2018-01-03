---
title: "Habilitando integração CLR | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d66238df770dfd647c3013441024409f15fdef9b
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="clr-integration---enabling"></a>Integração do CLR - habilitar
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O recurso de integração do common language runtime (CLR) está desativado por padrão e deve ser habilitado para usar objetos que são implementados usando a integração CLR. Para habilitar a integração CLR, use o **clr habilitado** opção do **sp_configure** procedimento de armazenado [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```sql  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 Você pode desabilitar a integração CLR definindo a **clr habilitado** opção como 0. Quando você desabilitar integração de CLR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deixará de executar todas as rotinas de CLR e descarregará todos os domínios de aplicativo.  
  
> [!NOTE]  
>  Para habilitar a integração CLR, você deve ter permissão ALTER SETTINGS servidor nível, que é mantida implicitamente por membros do **sysadmin** e **serveradmin** funções de servidor fixas.  
  
> [!NOTE]  
>  Computadores configurados com grandes quantidades de memória e um número grande de processadores podem falhar ao carregar o recurso de integração CLR do SQL Server na inicialização do servidor. Para resolver esse problema, inicie o servidor usando o **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção de inicialização de serviço e especifique um valor de memória grande o suficiente. Para obter mais informações, consulte [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Antes de habilitar integração CLR, você deve desabilitar o lightweight pooling. Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção clr enabled de configuração de servidor](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
