---
title: Permissões públicas de servidor | Microsoft Docs
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
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 237bfc653708c8f6e0968df82446f853db2ad96d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668524"
---
# <a name="server-public-permissions"></a>Permissões públicas de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra determina se a função de servidor público tem permissões de servidor. Todo logon criado no servidor é um membro da função de servidor público. Se esta condição for atendida, todo logon no servidor terá permissões de servidor.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Não conceda permissões de servidor à função de servidor público.  
  
> [!IMPORTANT]  
>  Depois que a instalação for concluída, a função **PUBLIC** terá a permissão **CONNECT** em todos os pontos de extremidade, exceto em **Conexão de Administrador Dedicada**. Isso é normal e não deve ser alterado. (O acesso é controlado pela permissão **CONNECT SQL** , que é concedida automaticamente quando novos logons são criados.)  
  
### <a name="for-more-information"></a>Para obter mais informações  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
