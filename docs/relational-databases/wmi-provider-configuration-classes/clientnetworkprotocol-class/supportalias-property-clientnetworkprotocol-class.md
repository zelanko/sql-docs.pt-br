---
title: Propriedade SupportAlias (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SupportAlias Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4cd3ba42974c65591f7920d5df8d7dd8a937d352
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040830"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Propriedade SupportAlias (classe ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém a propriedade booliana que especifica se o atual protocolo de rede especificado pela [método SetOrderValue (classe ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) dá suporte a aliases.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Um valor Booliano que especifica se o protocolo de rede de cliente dá suporte a aliases.  
  
 Se True, o protocolo de rede de cliente dá suporte a aliases.  
  
 Se False, o protocolo de rede de cliente não dá suporte a aliases.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
