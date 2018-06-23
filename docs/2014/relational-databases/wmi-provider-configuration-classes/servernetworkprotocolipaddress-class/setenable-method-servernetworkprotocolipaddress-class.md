---
title: Método SetEnable (classe ServerNetworkProtocolIPAddress) | Microsoft Docs
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
- SetEnable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: baa86deb-95dd-416f-b2c7-cec1dfb91ab4
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b51d13de41aa5fc038ddcd86fdc05a975aea7bc5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122800"
---
# <a name="setenable-method-servernetworkprotocolipaddress-class"></a>Método SetEnable (classe ServerNetworkProtocolIPAddress)
  Habilita o endereço IP.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetEnable()  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ServerNetworkProtocolIPAdress](servernetworkprotocolipaddress-class.md) que representa um endereço IP para o protocolo de rede na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  