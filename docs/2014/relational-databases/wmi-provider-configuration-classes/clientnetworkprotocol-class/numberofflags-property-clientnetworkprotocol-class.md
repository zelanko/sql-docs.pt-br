---
title: Propriedade NumberOfFlags (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NumberOfFlags Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 10a3ca3269b07206ef9d67f28de4e490e77140b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256098"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>Propriedade NumberOfFlags (classe ClientNetworkProtocol)
  Obtém o número de opções de sinalizador exigido pelo protocolo de rede do cliente especificado pelo [método SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `Uint32` que especifica o número de opções de sinalizador exigido pelo protocolo de rede de cliente referenciado pela propriedade `OrderValue`.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
