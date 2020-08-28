---
description: StreamWriteEnum
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c09a15f5c5aba9d36f038304b68cc1e64112ade3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988437"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de [fluxo](./stream-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Padrão. Grava a cadeia de caracteres de texto especificada (especificada pelo parâmetro de *dados* ) no objeto de **fluxo** .|  
|**adWriteLine**|1|Grava uma cadeia de caracteres de texto e um caractere separador de linha em um objeto de **fluxo** . Se a propriedade [LineSeparator](./lineseparator-property-ado.md) não for definida, isso retornará um erro em tempo de execução.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método WriteText](./writetext-method.md)