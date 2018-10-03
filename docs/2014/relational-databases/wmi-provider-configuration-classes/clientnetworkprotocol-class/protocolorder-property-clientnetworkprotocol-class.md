---
title: Propriedade ProtocolOrder (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: de7284c4023f7e658c37794d670356fd5b9c4025
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152448"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>Propriedade ProtocolOrder (classe ClientNetworkProtocol)
  Obtém o número de pedido do protocolo de rede do cliente atualmente referenciado como especificado pelo [método SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32` que especifica o número de pedido do protocolo de rede do cliente atualmente referenciado como definido pelo método `OrderValue`. Se o protocolo de rede de cliente estiver desabilitado, esse valor será zero.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)   
 [Configurando protocolos de rede do cliente e bibliotecas de rede](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
