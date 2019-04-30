---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0f42561d7b324a13068c14d0fc7971d3d46d83b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311780"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Padrão. Grava a cadeia de caracteres de texto especificado (especificado pela *dados* parâmetro) para o **Stream** objeto.|  
|**adWriteLine**|1|Grava uma cadeia de caracteres de texto e um caractere de separador de linha para um **Stream** objeto. Se o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade não está definida e, em seguida, isso retornará um erro de tempo de execução.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
