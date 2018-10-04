---
title: Propriedade Properties (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1464f236966f830125e62da65b3a645c99374a11
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219936"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Propriedade Properties (classe ClientNetworkProtocol)
  Obtém as propriedades associadas com o protocolo de rede do cliente atual especificado pela opção [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz de [classe ClientNetworkProtocolProperty](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) objetos que representam as propriedades com suporte pelo protocolo de rede atual do cliente que é referenciado pelo `OrderValue` propriedade.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do cliente e bibliotecas de rede](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
