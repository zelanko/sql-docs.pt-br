---
title: Usando o Database Mail em vez do SQL Mail | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b4ef5d4831d59ff8221a18e50c3ea43fa474ddb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="use-database-mail-instead-of-sql-mail"></a>Usando o Database Mail em vez do SQL Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta regra verifica a exibição do catálogo sys.configurations para determinar se a opção de configuração do servidor do SQL Mail XPs está definida como ON.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 O SQL Mail será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Para enviar email, use o Database Mail.  
  
 O SQL Mail é executado em processo de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se o SQL Mail ficar inoperante, o servidor também ficará. O Database Mail é executado fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um processo separado, é escalável e não requer a instalação de componentes de cliente MAPI estendido no servidor de produção.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
