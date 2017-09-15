---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 582f85d3ce45071cd283f05f5d595e10b5d1614c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica se o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto deve retornar depois que a conexão é estabelecida (de forma síncrona) ou antes (de forma assíncrona).  
  
|Constante|Valor|Description|  
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
