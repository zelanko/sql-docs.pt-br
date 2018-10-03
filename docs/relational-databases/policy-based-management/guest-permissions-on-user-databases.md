---
title: Permissões de convidado em bancos de dados de usuários | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 366ee3f80bacbd1cf17bcec7ed0c4e04ce892277
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787974"
---
# <a name="guest-permissions-on-user-databases"></a>Permissões de convidado em bancos de dados de usuários
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra determina se o usuário convidado tem permissão para acessar o banco de dados. Esta regra só se aplica a bancos de dados de usuários.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Revogue a permissão de usuário convidado para acessar o banco de dados se não for necessária.  
  
 O usuário convidado não pode ser descartado, mas pode ser desabilitado revogando sua permissão CONNECT com a execução de REVOKE CONNECT FROM GUEST em qualquer banco de dados que não seja mestre, tempdb ou msdb.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
