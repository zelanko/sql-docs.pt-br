---
title: Habilitando integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 37be3af485d43180c03c2214b8ee88b0535a4ea2
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703387"
---
# <a name="clr-integration---enabling"></a>Integração do CLR - habilitar
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O recurso de integração CLR (common language runtime) está desativado por padrão, e deve ser habilitado para usar objetos implementados com a integração CLR. Para habilitar a integração CLR, use o **clr habilitado** opção do **sp_configure** procedimento de armazenado [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção clr enabled de configuração de servidor](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
