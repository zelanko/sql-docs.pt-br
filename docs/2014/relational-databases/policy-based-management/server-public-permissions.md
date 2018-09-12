---
title: Permissões públicas de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1389d712ff00438a2e6251315e8ebcc55e7fbff2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813912"
---
# <a name="server-public-permissions"></a>Permissões públicas de servidor
  Esta regra determina se a função de servidor público tem permissões de servidor. Todo logon criado no servidor é um membro da função de servidor público. Se esta condição for atendida, todo logon no servidor terá permissões de servidor.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Não conceda permissões de servidor à função de servidor público.  
  
> [!IMPORTANT]  
>  Após a conclusão da instalação do **pública** função tem `CONNECT` permissão em todos os pontos de extremidade, exceto o **Conexão de administrador dedicada**. Isso é normal e não deve ser alterado. (O acesso é controlado usando o `CONNECT SQL` permissão é concedida automaticamente quando novos logons são criados.)  
  
### <a name="for-more-information"></a>Para obter mais informações  
 [Protegendo o SQL Server](../security/securing-sql-server.md)  
  
  
