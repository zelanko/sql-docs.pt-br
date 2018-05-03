---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3a974a46acd32a75773f7bd5034f30a62152499
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica se o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto deve retornar depois que a conexão é estabelecida (de forma síncrona) ou antes (de forma assíncrona).  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Abre a conexão de forma assíncrona. O [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) evento pode ser usado para determinar quando a conexão está disponível.|  
|**adConnectUnspecified**|-1|Padrão. Abre a conexão de forma síncrona.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
