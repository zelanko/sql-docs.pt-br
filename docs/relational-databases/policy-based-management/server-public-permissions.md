---
title: "Permissões públicas de servidor | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: "11"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3653a2895d4a2ce514a5f278a173ba8775dade6f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="server-public-permissions"></a>Permissões públicas de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta regra determina se a função de servidor público tem permissões de servidor. Todo logon criado no servidor é um membro da função de servidor público. Se esta condição for atendida, todo logon no servidor terá permissões de servidor.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Não conceda permissões de servidor à função de servidor público.  
  
> [!IMPORTANT]  
>  Depois que a instalação for concluída, a função **PUBLIC** terá a permissão **CONNECT** em todos os pontos de extremidade, exceto em **Conexão de Administrador Dedicada**. Isso é normal e não deve ser alterado. (O acesso é controlado pela permissão **CONNECT SQL** , que é concedida automaticamente quando novos logons são criados.)  
  
### <a name="for-more-information"></a>Para obter mais informações  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
