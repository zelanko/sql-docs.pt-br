---
description: StreamReadEnum
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: rothja
ms.author: jroth
ms.openlocfilehash: d9f685a80d822950a159ddb3fbc9f148489a723e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988467"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica se o fluxo inteiro ou a próxima linha deve ser lido a partir de um objeto de [fluxo](./stream-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Padrão. Lê todos os bytes do fluxo, da posição atual em diante para o marcador de [EOS](./eos-property.md) . Esse é o único valor de **StreamReadEnum** válido com fluxos binários (o[tipo](./type-property-ado-stream.md) é **adTypeBinary**).|  
|**adReadLine**|-2|Lê a próxima linha do fluxo (designada pela propriedade [LineSeparator](./lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Método Read](./read-method.md)  
    :::column-end:::
    :::column:::
        [Método ReadText](./readtext-method.md)  
    :::column-end:::
:::row-end:::