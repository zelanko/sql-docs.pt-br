---
title: Posicionamento do conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924439"
---
# <a name="recordset-positioning"></a>Posicionamento do conjunto de registros
Use a propriedade **AbsolutePosition** para mover para um registro, com base em sua posição ordinal no objeto **Recordset** , ou para determinar a posição ordinal do registro atual. O provedor deve dar suporte à funcionalidade apropriada para que essa propriedade esteja disponível.  
  
 O **AbsolutePosition** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **conjunto de registros**. Conforme mencionado anteriormente, você pode obter o número total de registros no objeto **Recordset** da propriedade **RecordCount** .  
  
 Quando você define a propriedade **AbsolutePosition** , mesmo que seja para um registro no cache atual, o ADO recarrega o cache com um novo grupo de registros, começando com o registro especificado. A propriedade **CacheSize** determina o tamanho desse grupo.  
  
> [!NOTE]
>  Você não deve usar a propriedade **AbsolutePosition** como um número de registro substituto. A posição de um determinado registro é alterada quando você exclui um registro anterior. Também não há nenhuma garantia de que um determinado registro terá o mesmo **AbsolutePosition** se o objeto **Recordset** for reconsultado ou reaberto. Indicadores são a maneira recomendada de reter e retornar a uma determinada posição e são a única maneira de posicionar em todos os tipos de objetos de **conjunto de registros** .
