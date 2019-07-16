---
title: Propriedade NumberOfFlags (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 38ee03d14250e49da21ae5be8526ae52f96ac380
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041194"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>Propriedade NumberOfFlags (classe ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém o número de opções de sinalizador exigido pelo protocolo de rede do cliente especificado pelo [método SetOrderValue (classe ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Um **Uint32** que especifica o número de opções de sinalizador exigido pelo protocolo de rede do cliente referenciado pelo valor de **OrderValue** propriedade.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
