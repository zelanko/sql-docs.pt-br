---
title: Método SetNumericalValue (classe ClientNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumericalValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: d4d6df52-9e68-4003-9e28-ece6716ba7f1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2f5459373689c17e0a55d8df0f02507bf24989ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245064"
---
# <a name="setnumericalvalue-method-clientnetworkprotocolproperty-class"></a>Método SetNumericalValue (classe ClientNetworkProtocolProperty)
  Define o valor numérico da propriedade atual referenciado pelo valor [PropertyIdx Property (classe ClientNetworkProtocolProperty) (classe ClientNetworkProtocolProperty)](clientnetworkprotocolproperty-class.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetNumericalValue [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocolProperty](clientnetworkprotocolproperty-class.md) que representa um atributo do protocolo de rede usado pelo cliente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*value*|Um valor `uint32` que especifica o valor numérico da propriedade referenciada.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
