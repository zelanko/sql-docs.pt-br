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
manager: craigg
ms.openlocfilehash: 8047d60d0a7b9b06a88a1e05673d4dba58d9e60f
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51215645"
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
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz dos objetos da [classe ServerNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) que representam as propriedades pelo protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
