---
description: Propriedade ProtocolOrder (classe ClientNetworkProtocol)
title: Propriedade ProtocolOrder (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2eef28c6250524757b4a3f23c625bb0c8fe02d71
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446301"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>Propriedade ProtocolOrder (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o número de pedido do protocolo de rede do cliente atualmente referenciado como especificado pelo [método SetOrderValue (classe ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** que especifica o número de pedido do protocolo de rede do cliente atualmente referenciado como definido pelo método **OrderValue** . Se o protocolo de rede de cliente estiver desabilitado, esse valor será zero.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)   
 [Configurando protocolos de cliente de servidor e bibliotecas de rede](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
