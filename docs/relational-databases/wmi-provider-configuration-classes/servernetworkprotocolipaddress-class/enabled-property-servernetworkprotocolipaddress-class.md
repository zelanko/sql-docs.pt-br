---
title: Propriedade (classe ServerNetworkProtocolIpAddress) habilitada | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95b9b7ef8901a20f524a88024e007721a4e20946
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Propriedade Enabled (classe ServerNetworkProtocolIpAddress)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém a propriedade booliana que especifica se um endereço IP está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 A [classe ServerNetworkProtocolIPAdress](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) que representa um endereço IP para o protocolo de rede na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se o endereço IP está habilitado: **true** se o endereço IP estiver habilitado, ou **false** se o endereço IP estiver desabilitado.  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
