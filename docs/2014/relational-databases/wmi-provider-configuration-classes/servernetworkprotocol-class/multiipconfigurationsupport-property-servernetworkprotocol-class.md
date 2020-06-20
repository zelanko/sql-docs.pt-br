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
ms.openlocfilehash: 80401a607c9155451a869082162affcca401ebca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059912"
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
 Um objeto de [Propriedade ProtocolName (classe ServerNetworkProtocol)](servernetworkprotocol-class.md) que representa o protocolo de rede usado pela instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se vários endereços IP têm suporte do protocolo de rede do servidor: `true` se vários endereços IP tiverem suporte do protocolo de rede do servidor ou `false` se vários endereços IP não tiverem suporte do protocolo de rede do servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
