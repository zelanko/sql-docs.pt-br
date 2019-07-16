---
title: Propriedade Properties (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 71e99af016ab114eecaa170374f9e07bf53bd3f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933664"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Propriedade Properties (classe ServerNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém as propriedades associadas com o protocolo de rede do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto [ServerNetworkProtocol Classe](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) que representa o protocolo de rede usado pela instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Uma matriz dos objetos da [classe ServerNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) que representam as propriedades pelo protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
