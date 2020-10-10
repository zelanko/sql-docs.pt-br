---
description: Propriedade ProtocolDLL (classe ClientNetworkProtocol)
title: Propriedade ProtocolDLL (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 54d992dd3d9b3604644f985f9e7db5f523b553f9
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888854"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>Propriedade ProtocolDLL (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o nome do arquivo .dll exigido pelo protocolo de rede especificado pela opção [Configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor da cadeia de caracteres que especifica o protocolo do arquivo .dll que é exigido pelo protocolo de rede do cliente.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de cliente de servidor e bibliotecas de rede](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
