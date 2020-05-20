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
author: rothja
ms.author: jroth
ms.openlocfilehash: 479bc032cf779752f11dccca73ee56fc05a8ebdd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759562"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Padrão. Grava a cadeia de caracteres de texto especificada (especificada pelo parâmetro de *dados* ) no objeto de **fluxo** .|  
|**adWriteLine**|1|Grava uma cadeia de caracteres de texto e um caractere separador de linha em um objeto de **fluxo** . Se a propriedade [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) não for definida, isso retornará um erro em tempo de execução.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
