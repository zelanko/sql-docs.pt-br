---
title: Possibilitando a Integração clr | Microsoft Docs
description: O Microsoft SQL Server que hospeda clr é chamado de integração CLR, que é desativado por padrão. Use o procedimento armazenado sp_configure para permitir a integração da CLR.
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
ms.openlocfilehash: 7d161135c8c8b0c7d7932eb08aa98509efc4bc45
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488094"
---
# <a name="clr-integration---enabling"></a>Integração CLR – Habilitar
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  O recurso de integração CLR (common language runtime) está desativado por padrão, e deve ser habilitado para usar objetos implementados com a integração CLR. Para habilitar a integração CLR, use **sp_configure** a opção [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **habilitada clr** do sp_configure procedimento armazenado em :  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Você pode desativar a integração CLR definindo a opção **habilitada clr** para 0. Quando você desativa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a integração CLR, deixa de executar todas as rotinas CLR definidas pelo usuário e descarrega todos os domínios do aplicativo. Os recursos que dependem do CLR, como o tipo `FORMAT` de dados **hierárquico,** a função, a replicação e o gerenciamento baseado em políticas, não são afetados por essa configuração e continuarão a funcionar.
  
> [!NOTE]  
>  Para habilitar a integração clr, você deve ter a permissão de nível de servidor ALTER SETTINGS, que é implicitamente mantida por membros das funções de servidor fixo **sysadmin** e **serveradmin.**  
  
> [!NOTE]  
>  Computadores configurados com grandes quantidades de memória e um número grande de processadores podem falhar ao carregar o recurso de integração CLR do SQL Server na inicialização do servidor. Para resolver esse problema, inicie o servidor usando a opção de inicialização de serviço **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especifique um valor de memória grande o suficiente. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Antes de habilitar integração CLR, você deve desabilitar o lightweight pooling. Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;&#40;&#40;&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [opção de configuração do servidor habilitado clr](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURAR &#40;&#41;Transact-SQL](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Funções em nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
