---
title: Cursores roláveis e isolamento da transação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbbcdf0c9ce2c7e37072502ae49b43dc20d15a9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
|Insert (inserir)|Talvez [b]|não|Não|Não|Não|não|  
|Update (atualizar)|Talvez [b]|não|Não|Não|Não|não|  
|Delete (excluir)|Talvez [b]|não|Não|Não|Não|não|  
|Controlado por conjunto de chaves|||||||  
|Insert (inserir)|Talvez [b]|não|Não|Não|Não|não|  
|Update (atualizar)|Sim|Sim|Sim|Sim|Não|não|  
|Delete (excluir)|Talvez [b]|Sim|Sim|Sim|Não|não|  
|Dinâmicos|||||||  
|Insert (inserir)|Sim|Sim|Sim|Sim|Sim|não|  
|Update (atualizar)|Sim|Sim|Sim|Sim|Não|não|  
|Delete (excluir)|Sim|Sim|Sim|Sim|Não|não|  
  
 [a] as letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da transação (no qual a alteração foi feita) é irrelevante.  
  
 RU: Leitura não confirmada  
  
 RC: Leitura confirmada  
  
 RR: Leitura repetida  
  
 S: serializável  
  
 [b] depende de como o cursor é implementado. Se o cursor pode detectar alterações é relatado com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.
