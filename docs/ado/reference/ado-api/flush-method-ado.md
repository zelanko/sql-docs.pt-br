---
title: "Método (ADO) Flush | Microsoft Docs"
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
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94a5e1ced6f0b302253298dcbfb9cd345b9f5bfe
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="flush-method-ado"></a>Método de liberação (ADO)
Força o conteúdo do [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) restantes no buffer de ADO para o objeto subjacente com a qual o **fluxo** está associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Remarks  
 Esse método pode ser usado para enviar o conteúdo do buffer de fluxo para o objeto subjacente: por exemplo, o nó ou o arquivo representado pela URL que é a origem do **fluxo** objeto. Esse método deve ser chamado quando você deseja garantir que todas as alterações que foram feitas para o conteúdo de um **fluxo** foram gravados. No entanto, com o ADO não é geralmente necessário chamar **liberar**, como ADO continuamente libera o buffer tanto quanto possível em segundo plano. Altera para o conteúdo de um **fluxo** são feitas automaticamente, não armazenado em cache até **liberar** é chamado.  
  
 Fechando uma **fluxo** com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método libera o conteúdo de um **fluxo** automaticamente; existe, é necessário chamar explicitamente **liberar**imediatamente antes do **fechar**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
