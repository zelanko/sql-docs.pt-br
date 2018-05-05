---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
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
ms.openlocfilehash: 352317f63627038d8b415dce5095aa1570a7f7f8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
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
