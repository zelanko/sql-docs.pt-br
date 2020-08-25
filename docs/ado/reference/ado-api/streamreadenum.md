---
description: StreamReadEnum
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: c0a0e8d93742574e9a2975b99d15c18500684e60
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777175"
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