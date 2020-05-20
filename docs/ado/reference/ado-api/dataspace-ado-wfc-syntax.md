---
title: DataSpace (sintaxe ADO-WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: rothja
ms.author: jroth
ms.openlocfilehash: c736dc38949945a6e62e5121c4edf4b98dfbc7fc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763447"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO – Sintaxe WFC)
O método **CreateObject** da classe **DataSpace** especifica um objeto comercial para processar as solicitações de aplicativo cliente (*ProgID*) e o protocolo de comunicação e o servidor (*conexão*). **CreateObject** retorna um objeto [objectproxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) que representa o servidor.  
  
## <a name="package-commswfcdata"></a>pacote com. ms. wfc. Data  
  
### <a name="constructor"></a>Construtor  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
