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
ms.workload: Inactive
ms.openlocfilehash: 57b9c297b40c08986737e6606e89546ffe17b3e7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
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
