---
title: Cursores roláveis e isolamento da transação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5510eb58315f70195eb40390edec1766c350fb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468584"
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
  
 A tabela a seguir resume a capacidade de detectar as alterações feitas por si só, por outras operações em sua própria transação e por outras transações de cada tipo de cursor. A visibilidade das alterações de última depende o tipo de cursor e o nível de isolamento da transação que contém o cursor.  
  
|Cursor type\action|Self|O proprietário<br /><br /> Txn|Outra<br /><br /> Txn<br /><br /> (RU[a])|Outra<br /><br /> Txn<br /><br /> (RC[a])|Outra<br /><br /> Txn<br /><br /> (RR[a])|Outra<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert|Maybe[b]|Não |Não|Não|Não|Não|  
|Update|Maybe[b]|Não|Não |Não |Não|Não |  
|DELETE|Maybe[b]|Não |Não |Não |Não|Não|  
|Controlado por conjunto de chaves|||||||  
|Insert|Maybe[b]|Não|Não |Não |Não |Não|  
|Update|Sim|Sim|Sim|Sim|Não|Não |  
|DELETE|Maybe[b]|Sim|Sim|Sim|Não |Não|  
|Dinâmico|||||||  
|Insert|Sim|Sim|Sim|Sim|Sim|Não |  
|Update|Sim|Sim|Sim|Sim|Não|Não |  
|DELETE|Sim|Sim|Sim|Sim|Não |Não |  
  
 [a] as letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da transação (no qual a alteração foi feita) é irrelevante.  
  
 RU: Leitura não confirmada  
  
 RC: Leitura confirmada  
  
 RR: Leitura repetida  
  
 S:  Serializável  
  
 [b] depende de como o cursor é implementado. Se o cursor pode detectar essas alterações é relatada com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.
