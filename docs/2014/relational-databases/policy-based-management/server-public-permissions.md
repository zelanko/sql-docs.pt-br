---
title: Permissões públicas de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 13efadee3de21493d979f800f40a279581cadd03
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246376"
---
# <a name="server-public-permissions"></a>Permissões públicas de servidor
  Esta regra determina se a função de servidor público tem permissões de servidor. Todo logon criado no servidor é um membro da função de servidor público. Se esta condição for atendida, todo logon no servidor terá permissões de servidor.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Não conceda permissões de servidor à função de servidor público.  
  
> [!IMPORTANT]  
>  Após a conclusão da instalação do **pública** função tem `CONNECT` permissão em todos os pontos de extremidade, exceto o **Conexão de administrador dedicada**. Isso é normal e não deve ser alterado. (O acesso é controlado usando o `CONNECT SQL` permissão é concedida automaticamente quando novos logons são criados.)  
  
### <a name="for-more-information"></a>Para obter mais informações  
 [Protegendo o SQL Server](../security/securing-sql-server.md)  
  
  
