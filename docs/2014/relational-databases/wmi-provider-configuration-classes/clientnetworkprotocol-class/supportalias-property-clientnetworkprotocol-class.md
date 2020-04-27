---
title: Propriedade SupportAlias (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: d28ec166f8954b874f98b7f9f441280ab9064f1f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62826752"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Propriedade SupportAlias (classe ClientNetworkProtocol)
  Obtém a propriedade booliana que especifica se o protocolo de rede atual especificado pelo [método Setordenavalue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) dá suporte a aliases.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor Booliano que especifica se o protocolo de rede de cliente dá suporte a aliases.  
  
 Se True, o protocolo de rede de cliente dá suporte a aliases.  
  
 Se False, o protocolo de rede de cliente não dá suporte a aliases.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
