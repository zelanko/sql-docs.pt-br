---
title: Propriedade Properties (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6497305d0a0d9a303df0f46e74914b3467243cdf
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217684"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Propriedade Properties (classe ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém as propriedades associadas com o protocolo de rede do cliente atual especificado pela opção [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz dos objetos da [classe ClientNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) que representam as propriedades com suporte do protocolo de rede de cliente atual que é referenciado pela propriedade **OrderValue** .  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do cliente e bibliotecas de rede](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
