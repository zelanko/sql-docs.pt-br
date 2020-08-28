---
description: Emitir comandos para o Provedor de Dados subjacente
title: Emitindo comandos para o Provedor de Dados subjacente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: rothja
ms.author: jroth
ms.openlocfilehash: d4f1db51d54b69bf42fe185d30b78df57b89df39
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980427"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos para o Provedor de Dados subjacente
Qualquer comando que não comece com a forma será passado para o provedor de dados. Isso é equivalente a emitir um comando de forma no formato "forma {comando do provedor}". Esses comandos *não* precisam produzir um conjunto de **registros**. Por exemplo, "forma {DROP TABLE MyTable} é um comando de forma perfeitamente válido, supondo que o provedor de dados ofereça suporte a DROP TABLE.  
  
 Esse recurso permite que os comandos normais do provedor e os comandos de forma compartilhem a mesma conexão e transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](./data-shaping-example.md)   
 [Gramática forma formal](./formal-shape-grammar.md)   
 [Modelar comandos em geral](./shape-commands-in-general.md)