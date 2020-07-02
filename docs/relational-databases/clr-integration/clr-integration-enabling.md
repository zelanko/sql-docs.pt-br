---
title: Habilitando a integração CLR | Microsoft Docs
description: Microsoft SQL Server Hospedagem de CLR é chamada de integração CLR, que é desabilitada por padrão. Use o procedimento armazenado sp_configure para habilitar a integração CLR.
ms.custom: ''
ms.date: 09/17/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0200cec59d12f8311a280bd16b3cb1c5b0eb5374
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727623"
---
# <a name="clr-integration---enabling"></a>Integração CLR – Habilitar
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  O recurso de integração CLR (common language runtime) está desativado por padrão, e deve ser habilitado para usar objetos implementados com a integração CLR. Para habilitar a integração CLR, use a opção **CLR Enabled** do procedimento armazenado **sp_configure** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] :  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Você pode desabilitar a integração CLR definindo a opção **CLR Enabled** como 0. Quando você desabilita a integração CLR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interrompe a execução de todas as rotinas CLR definidas pelo usuário e descarrega todos os domínios de aplicativo. Os recursos que dependem do CLR, como o tipo de dados **hierarchyid** , a `FORMAT` função, a replicação e o gerenciamento baseado em políticas, não são afetados por essa configuração e continuarão a funcionar.
  
> [!NOTE]  
>  Para habilitar a integração CLR, você deve ter a permissão ALTER SETTINGS no nível do servidor, que é mantida implicitamente por membros das funções de servidor fixas **sysadmin** e **ServerAdmin** .  
  
> [!NOTE]  
>  Computadores configurados com grandes quantidades de memória e um número grande de processadores podem falhar ao carregar o recurso de integração CLR do SQL Server na inicialização do servidor. Para resolver esse problema, inicie o servidor usando a opção de inicialização de serviço **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especifique um valor de memória grande o suficiente. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Antes de habilitar integração CLR, você deve desabilitar o lightweight pooling. Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção de configuração de servidor CLR Enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [CONCEDER &#40;&#41;Transact-SQL](../../t-sql/statements/grant-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
