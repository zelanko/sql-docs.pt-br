---
title: Propriedade (classe ServerNetworkProtocolIpAddress) habilitada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 655acfd106800927bbec8b2fa8021a3b2ba4be87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117096"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Propriedade Enabled (classe ServerNetworkProtocolIpAddress)
  Obtém a propriedade booliana que especifica se um endereço IP está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.Enabled [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ServerNetworkProtocolIPAdress](servernetworkprotocolipaddress-class.md) que representa um endereço IP para o protocolo de rede na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se o endereço IP está habilitado: `true` se o endereço IP estiver habilitado, ou `false` se o endereço IP estiver desabilitado.  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  