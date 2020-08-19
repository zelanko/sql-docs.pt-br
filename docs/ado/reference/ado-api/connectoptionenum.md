---
description: ConnectOptionEnum
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: rothja
ms.author: jroth
ms.openlocfilehash: 71142aac94003987267a6d4a6b30d2c9d17c1bfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444418"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica se o método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) de um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) deve retornar depois que a conexão é estabelecida (de forma síncrona) ou anterior (assincronamente).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Abre a conexão de forma assíncrona. O evento [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) pode ser usado para determinar quando a conexão está disponível.|  
|**adConnectUnspecified**|-1|Padrão. Abre a conexão de forma síncrona.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
