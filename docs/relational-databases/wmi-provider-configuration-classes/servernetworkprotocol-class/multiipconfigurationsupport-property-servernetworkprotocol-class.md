---
description: Propriedade MultiIpConfigurationSupport (classe ServerNetworkProtocol)
title: Propriedade MultiIpConfigurationSupport (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: da02aefabf6096712b4d6ccb06622892a20dbbed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472823"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>Propriedade MultiIpConfigurationSupport (classe ServerNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém uma propriedade booliana que especifica se vários endereços IP têm suporte de um protocolo de rede do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto de [Propriedade ProtocolName (classe ServerNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md) que representa o protocolo de rede usado pela instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se há suporte para vários endereços IP pelo protocolo de rede do servidor: **true** se houver suporte para vários endereços IP pelo protocolo de rede do servidor ou **false** se não houver suporte para vários endereços IP pelo protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
