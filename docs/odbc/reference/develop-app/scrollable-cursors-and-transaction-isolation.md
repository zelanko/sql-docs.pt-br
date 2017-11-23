---
title: "Cursores roláveis e isolamento da transação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4db2f357942eb7bab34a17e8f9c03e442731055
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Cursores roláveis e isolamento da transação
A tabela a seguir lista os fatores que governam a visibilidade das alterações.  
  
|Alterações feitas por:|Visibilidade depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementação de cursor|  
|Outras instruções na mesma transação|Tipo de cursor|  
|Instruções em outras transações|Tipo de cursor, o nível de isolamento da transação|  
  
 Esses fatores são mostrados na ilustração a seguir.  
  
 ![Fatores que governam a visibilidade das alterações](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 A tabela a seguir resume a capacidade de cada tipo de cursor de detectar alterações feitas por si só, por outras operações em sua própria transação e por outras transações. A visibilidade das alterações de última depende do tipo de cursor e o nível de isolamento da transação que contém o cursor.  
  
|Type\action de cursor|Self|O proprietário<br /><br /> Txn|Outra<br /><br /> Txn<br /><br /> (RU[a])|Outra<br /><br /> Txn<br /><br /> (RC[a])|Outra<br /><br /> Txn<br /><br /> (RR[a])|Outra<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert (inserir)|Talvez [b]|Não|Não|Não|Não|Não|  
|Update (atualizar)|Talvez [b]|Não|Não|Não|Não|Não|  
|DELETE|Talvez [b]|Não|Não|Não|Não|Não|  
|Controlado por conjunto de chaves|||||||  
|Insert (inserir)|Talvez [b]|Não|Não|Não|Não|Não|  
|Update (atualizar)|Sim|Sim|Sim|Sim|Não|Não|  
|DELETE|Talvez [b]|Sim|Sim|Sim|Não|Não|  
|Dinâmicos|||||||  
|Insert (inserir)|Sim|Sim|Sim|Sim|Sim|Não|  
|Update (atualizar)|Sim|Sim|Sim|Sim|Não|Não|  
|DELETE|Sim|Sim|Sim|Sim|Não|Não|  
  
 [a] as letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da transação (no qual a alteração foi feita) é irrelevante.  
  
 RU: Leitura não confirmada  
  
 RC: Leitura confirmada  
  
 RR: Leitura repetida  
  
 S: serializável  
  
 [b] depende de como o cursor é implementado. Se o cursor pode detectar alterações é relatado com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.
