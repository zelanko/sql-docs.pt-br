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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bd31cf4758415cc235942607319a26c1a283437
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545411"
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
  
  
