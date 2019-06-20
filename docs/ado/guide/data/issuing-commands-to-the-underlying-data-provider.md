---
title: Emissão de comandos para o provedor de dados subjacente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 231d9ced5bf370b8ee7c507e930e6961cfbed5a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700573"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos para o Provedor de Dados subjacente
Qualquer comando que não começa com a forma é passado para o provedor de dados. Isso é equivalente a emitir um comando de forma na forma "Forma {comando do provedor}". Esses comandos fazer *não* deve produzir uma **conjunto de registros**. Por exemplo, "forma {DROP TABLE MyTable} é um comando de forma perfeitamente válida, supondo que o provedor de dados oferece suporte a DROP TABLE.  
  
 Essa funcionalidade permite que os comandos de provedor normal e comandos de forma a compartilhar a mesma conexão e transação.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
