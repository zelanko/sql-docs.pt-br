---
title: Propriedade MultiIpConfigurationSupport (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3a6813371e7641af1369f94f875ca0d9f96ad3a3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350623"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>Propriedade MultiIpConfigurationSupport (classe ServerNetworkProtocol)
  Obtém uma propriedade booliana que especifica se vários endereços IP têm suporte de um protocolo de rede do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um [propriedade ProtocolName (classe ServerNetworkProtocol)](servernetworkprotocol-class.md) que representa o protocolo de rede usado pela instância do objeto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se vários endereços IP têm suporte do protocolo de rede do servidor: `true` se vários endereços IP tiverem suporte do protocolo de rede do servidor ou `false` se vários endereços IP não tiverem suporte do protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
