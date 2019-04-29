---
title: Método flush (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66deae3833a738075259928855881f87b64ef0dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028094"
---
# <a name="flush-method-ado"></a>Método Flush (ADO)
Força o conteúdo do [Stream](../../../ado/reference/ado-api/stream-object-ado.md) restantes no buffer ADO para o objeto subjacente com a qual o **Stream** está associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Comentários  
 Esse método pode ser usado para enviar o conteúdo do buffer de fluxo para o objeto subjacente: por exemplo, o nó ou o arquivo representado pela URL que é a origem do **Stream** objeto. Esse método deve ser chamado quando você deseja garantir que todas as alterações que foram feitas ao conteúdo de um **Stream** foram gravados. No entanto, com o ADO não é geralmente necessário chamar **liberar**, como ADO continuamente libera o buffer tanto quanto possível em segundo plano. Altera para o conteúdo de um **Stream** são feitas automaticamente, não armazenado em cache até **liberar** é chamado.  
  
 Fechando uma **Stream** com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método libera o conteúdo de um **Stream** automaticamente; não há, é necessário chamar explicitamente **liberar**imediatamente antes **fechar**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
