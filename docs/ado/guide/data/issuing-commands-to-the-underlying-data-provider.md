---
title: Emitir comandos para o provedor de dados subjacente | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24498f4d57627a1a7fb265a22703c0e9f8e581af
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos para o provedor de dados subjacente
Qualquer comando que não começam com a forma é passado para o provedor de dados. Isso é equivalente a emitir um comando de forma no formato "Forma {comando do provedor}". Esses comandos não *não* de produzir um **registros**. Por exemplo, "forma {DROP TABLE MyTable} é um comando de forma perfeitamente válida, supondo que o provedor de dados oferece suporte a DROP TABLE.  
  
 Esse recurso permite que os comandos de provedor normal e comandos de forma para compartilhar a mesma conexão e transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
