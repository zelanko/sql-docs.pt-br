---
title: Propriedade Properties (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Properties Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 62dc2149afae84eab6fa236d5601c50c9b99c1cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122575"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Propriedade Properties (classe ServerNetworkProtocol)
  Obtém as propriedades associadas com o protocolo de rede do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto [ServerNetworkProtocol Classe](servernetworkprotocol-class.md) que representa o protocolo de rede usado pela instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz dos objetos da [classe ServerNetworkProtocolProperty](../servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) que representam as propriedades pelo protocolo de rede do servidor.  
  
## <a name="remarks"></a>Remarks  
  