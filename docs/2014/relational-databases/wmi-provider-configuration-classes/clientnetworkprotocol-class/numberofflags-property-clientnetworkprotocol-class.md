---
title: Propriedade NumberOfFlags (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7847a5424b81efca1fcaff6b7dab899023204a7b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062664"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>Propriedade NumberOfFlags (classe ClientNetworkProtocol)
  Obtém o número de opções de sinalizador exigidas pelo protocolo de rede do cliente especificado pelo [Método SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `Uint32` que especifica o número de opções de sinalizador exigido pelo protocolo de rede de cliente referenciado pela propriedade `OrderValue`.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
