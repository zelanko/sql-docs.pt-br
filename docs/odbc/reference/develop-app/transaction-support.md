---
title: Suporte a transações | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0b5e33f94c5452a2062f7c18339f27c8da73fa9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086061"
---
# <a name="transaction-support"></a>Suporte à transação
O grau de suporte para transações é definido pelo driver. O ODBC foi projetado para ser implementado em um banco de dados de um único usuário ou área de trabalho que não precise gerenciar várias atualizações para eles. Além disso, alguns bancos de dados que dão suporte a transações fazem isso apenas para as instruções DML (linguagem de manipulação de data) do SQL; há restrições ou semântica de transação especial em relação ao uso de DDL (linguagem de definição de dados) quando uma transação está ativa. Ou seja, pode haver suporte a transações para várias atualizações simultâneas em tabelas, mas não para alterar o número e a definição de tabelas durante uma transação.  
  
 Um aplicativo determina se as transações têm suporte, se o DDL pode ser incluído em uma transação e quaisquer efeitos especiais de inclusão de DDL em uma transação, chamando **SQLGetInfo** com a opção SQL_TXN_CAPABLE. Para obter mais informações, consulte a descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Se o driver não oferecer suporte a transações, mas o aplicativo tiver a capacidade (usando uma API diferente do ODBC) para bloquear e desbloquear dados, os aplicativos poderão obter suporte a transações bloqueando e desbloqueando registros e tabelas conforme necessário. Para implementar o exemplo de transferência de conta, o aplicativo bloquearia os registros de ambas as contas, copiaria os valores atuais, debitará a primeira conta, creditará a segunda conta e desbloqueará os registros. Se alguma das etapas falhar, o aplicativo redefinirá as contas usando as cópias.  
  
 Até mesmo fontes de dados que dão suporte a transações podem não ser capazes de dar suporte a mais de uma transação por vez em um ambiente específico. Os aplicativos chamam **SQLGetInfo** com a opção SQL_MULTIPLE_ACTIVE_TXN para determinar se uma fonte de dados pode dar suporte a transações ativas simultâneas em mais de uma conexão no mesmo ambiente. Como há uma transação por conexão, isso só é interessante para aplicativos que têm várias conexões com a mesma fonte de dados.
