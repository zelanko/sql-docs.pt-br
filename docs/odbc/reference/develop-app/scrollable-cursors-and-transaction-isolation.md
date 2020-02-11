---
title: Cursores roláveis e isolamento de transação | Microsoft Docs
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
ms.openlocfilehash: 92e3694690ef1cba210da29766e7528762e691f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061597"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Cursores roláveis e isolamento da transação
A tabela a seguir lista os fatores que regem a visibilidade das alterações.  
  
|Alterações feitas por:|A visibilidade depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementação de cursor|  
|Outras instruções na mesma transação|Tipo de cursor|  
|Instruções em outras transações|Tipo de cursor, nível de isolamento da transação|  
  
 Esses fatores são mostrados na ilustração a seguir.  
  
 ![Fatores que governam a visibilidade das alterações](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 A tabela a seguir resume a capacidade de cada tipo de cursor detectar alterações feitas por si só, por outras operações em sua própria transação e por outras transações. A visibilidade das últimas alterações depende do tipo de cursor e do nível de isolamento da transação que contém o cursor.  
  
|Type\action do cursor|Auto-restauração|Tiver<br /><br /> TXN|Outra<br /><br /> TXN<br /><br /> (RU [a])|Outra<br /><br /> TXN<br /><br /> (RC [a])|Outra<br /><br /> TXN<br /><br /> (RR [a])|Outra<br /><br /> TXN<br /><br /> (S [a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert|Talvez [b]|Não|Não|Não|Não|Não|  
|Atualizar|Talvez [b]|Não|Não|Não|Não|Não|  
|Excluir|Talvez [b]|Não|Não|Não|Não|Não|  
|Controlado por conjunto de chaves|||||||  
|Insert|Talvez [b]|Não|Não|Não|Não|Não|  
|Atualizar|Sim|Sim|Sim|Sim|Não|Não|  
|Excluir|Talvez [b]|Sim|Sim|Sim|Não|Não|  
|Dinâmico|||||||  
|Insert|Sim|Sim|Sim|Sim|Sim|Não|  
|Atualizar|Sim|Sim|Sim|Sim|Não|Não|  
|Excluir|Sim|Sim|Sim|Sim|Não|Não|  
  
 [a] as letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da outra transação (no qual a alteração foi feita) é irrelevante.  
  
 RU: leitura não confirmada  
  
 RC: leitura confirmada  
  
 RR: leitura repetida  
  
 S: serializável  
  
 [b] depende de como o cursor é implementado. Se o cursor puder detectar essas alterações é relatado por meio da opção SQL_STATIC_SENSITIVITY em **SQLGetInfo**.
