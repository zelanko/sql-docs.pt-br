---
title: Propriedade SupportAlias (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2bfb677ba05bc5303c706d65dd2dda70eb67d23d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082566"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Propriedade SupportAlias (classe ClientNetworkProtocol)
  Obtém a propriedade booliana que especifica se o atual protocolo de rede especificado pela [método SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) dá suporte a aliases.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor Booliano que especifica se o protocolo de rede de cliente dá suporte a aliases.  
  
 Se True, o protocolo de rede de cliente dá suporte a aliases.  
  
 Se False, o protocolo de rede de cliente não dá suporte a aliases.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
