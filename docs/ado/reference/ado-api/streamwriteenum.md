---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36c18f5452a07e5dc44a9396ee993a163b98d3bd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Padrão. Grava a cadeia de caracteres de texto especificado (especificado pelo *dados* parâmetro) para o **fluxo** objeto.|  
|**adWriteLine**|1|Grava uma cadeia de caracteres de texto e um caractere de separador de linha para um **fluxo** objeto. Se o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade não está definida e, em seguida, isso retornará um erro de tempo de execução.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
