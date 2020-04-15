---
title: Cursores roláveis e isolamento de transações | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304217"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Cursores roláveis e isolamento da transação
A tabela a seguir lista os fatores que regem a visibilidade das mudanças.  
  
|Alterações feitas por:|A visibilidade depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementação do cursor|  
|Outras declarações na mesma transação|Tipo de cursor|  
|Declarações em outras transações|Tipo de cursor, nível de isolamento de transações|  
  
 Esses fatores são mostrados na ilustração a seguir.  
  
 ![Fatores que governam a visibilidade das alterações](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 A tabela a seguir resume a capacidade de cada tipo de cursor de detectar alterações feitas por si só, por outras operações em sua própria transação e por outras transações. A visibilidade das últimas alterações depende do tipo de cursor e do nível de isolamento da transação que contém o cursor.  
  
|Tipo de cursor\ação|Auto|Próprio<br /><br /> Rio Txn|Othr<br /><br /> Rio Txn<br /><br /> (RU[a])|Othr<br /><br /> Rio Txn<br /><br /> (RC[a])|Othr<br /><br /> Rio Txn<br /><br /> (RR[a])|Othr<br /><br /> Rio Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Inserir|Talvez[b]|Não|Não|Não|Não|Não|  
|Atualizar|Talvez[b]|Não|Não|Não|Não|Não|  
|Excluir|Talvez[b]|Não|Não|Não|Não|Não|  
|Controlado por conjunto de chaves|||||||  
|Inserir|Talvez[b]|Não|Não|Não|Não|Não|  
|Atualizar|Sim|Sim|Sim|Sim|Não|Não|  
|Excluir|Talvez[b]|Sim|Sim|Sim|Não|Não|  
|Dinâmico|||||||  
|Inserir|Sim|Sim|Sim|Sim|Sim|Não|  
|Atualizar|Sim|Sim|Sim|Sim|Não|Não|  
|Excluir|Sim|Sim|Sim|Sim|Não|Não|  
  
 [a] As letras entre parênteses indicam o nível de isolamento da transação que contém o cursor; o nível de isolamento da outra transação (em que a alteração foi feita) é irrelevante.  
  
 RU: Leia não comprometido  
  
 RC: Leia comprometido  
  
 RR: Leitura repetitiva  
  
 S: Serializable  
  
 [b] Depende de como o cursor é implementado. Se o cursor pode detectar tais alterações é relatado através da opção SQL_STATIC_SENSITIVITY no **SQLGetInfo**.
