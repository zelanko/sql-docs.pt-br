---
description: Método Flush (ADO)
title: Método Flush (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a76817a6219a506ef1158e94b7ffbf2fae6f629f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972977"
---
# <a name="flush-method-ado"></a>Método Flush (ADO)
Força o conteúdo do [fluxo](./stream-object-ado.md) restante no buffer do ADO para o objeto subjacente ao qual o **fluxo** está associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Comentários  
 Esse método pode ser usado para enviar o conteúdo do buffer de fluxo para o objeto subjacente: por exemplo, o nó ou arquivo representado pela URL que é a origem do objeto de **fluxo** . Esse método deve ser chamado quando você deseja garantir que todas as alterações feitas no conteúdo de um **fluxo** tenham sido gravadas. No entanto, com o ADO, normalmente não é necessário chamar **flush**, pois o ADO libera continuamente seu buffer o máximo possível em segundo plano. As alterações no conteúdo de um **fluxo** são feitas automaticamente, não armazenadas em cache até que a **liberação** seja chamada.  
  
 Fechar um **fluxo** com o método [Close](./close-method-ado.md) libera automaticamente o conteúdo de um **fluxo** ; Não é necessário chamar explicitamente a **liberação** imediatamente antes de **fechar**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)