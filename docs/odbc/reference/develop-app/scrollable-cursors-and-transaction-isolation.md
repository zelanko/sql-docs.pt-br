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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662344"
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
  
|Cursor type\action|Self|O proprietário<br /><br /> Trans.|Outra<br /><br /> Trans.<br /><br /> (RU[a])|Outra<br /><br /> Trans.<br /><br /> (RC[a])|Outra<br /><br /> Trans.<br /><br /> (RR[a])|Outra<br /><br /> Trans.<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert|Talvez [b]|não|não|não|não|não|  
|Update|Talvez [b]|não|não|não|não|não|  
|DELETE|Talvez [b]|não|não|não|não|não|  
|Controlado por conjunto de chaves|||||||  
|Insert|Talvez [b]|não|não|não|não|não|  
|Update|Sim|Sim|Sim|Sim|não|não|  
|DELETE|Talvez [b]|Sim|Sim|Sim|não|não|  
|Dinâmicos|||||||  
|Insert|Sim|Sim|Sim|Sim|Sim|não|  
|Update|Sim|Sim|Sim|Sim|não|não|  
|DELETE|Sim|Sim|Sim|Sim|não|não|  
  
 [a] as letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da transação (no qual a alteração foi feita) é irrelevante.  
  
 RU: Leitura não confirmada  
  
 RC: Leitura confirmada  
  
 RR: Leitura repetida  
  
 S: serializável  
  
 [b] depende de como o cursor é implementado. Se o cursor pode detectar essas alterações é relatada com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.
