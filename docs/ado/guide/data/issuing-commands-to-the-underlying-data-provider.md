---
title: Emitir comandos para o provedor de dados subjacente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19327273acb2d39875a0d85af5a157a240cf4c67
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos para o provedor de dados subjacente
Qualquer comando que não começam com a forma é passado para o provedor de dados. Isso é equivalente a emitir um comando de forma no formato "Forma {comando do provedor}". Esses comandos não *não* de produzir um **registros**. Por exemplo, "forma {DROP TABLE MyTable} é um comando de forma perfeitamente válida, supondo que o provedor de dados oferece suporte a DROP TABLE.  
  
 Esse recurso permite que os comandos de provedor normal e comandos de forma para compartilhar a mesma conexão e transação.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
