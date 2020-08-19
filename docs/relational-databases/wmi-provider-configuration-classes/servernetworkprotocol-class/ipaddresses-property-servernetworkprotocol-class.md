---
description: Propriedade IpAddresses (classe ServerNetworkProtocol)
title: Propriedade IpAddresses (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IpAddresses Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d499e84bef9a88ddb094586f6ff61904ef6f42ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446213"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>Propriedade IpAddresses (classe ServerNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém os endereços IP associados com o protocolo de rede do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.IpAddresses [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto **ServerNetworkProtocol** que representa o protocolo de rede usado pela instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz de objetos de [classe ServerNetworkProtocolIPAdress](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) que representam os endereços IP com suporte no protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
