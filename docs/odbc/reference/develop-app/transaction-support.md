---
title: Suporte à transação | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297974"
---
# <a name="transaction-support"></a>Suporte à transação
O grau de suporte para transações é definido pelo driver. O ODBC foi projetado para ser implementado em um banco de dados de um único usuário ou desktop que não precisa gerenciar várias atualizações de seus dados. Além disso, alguns bancos de dados que suportam transações o fazem apenas para as declarações dml (Data Manipulation Language, linguagem de manipulação de dados) do SQL; existem restrições ou semântica de transações especiais em relação ao uso do DDL (Data Definition Language, linguagem de definição de dados) quando uma transação está ativa. Ou seja, pode haver suporte a transações para várias atualizações simultâneas para tabelas, mas não para alterar o número e a definição de tabelas durante uma transação.  
  
 Um aplicativo determina se as transações são suportadas, se o DDL pode ser incluído em uma transação e quaisquer efeitos especiais de incluir o DDL em uma transação, ligando para o **SQLGetInfo** com a opção SQL_TXN_CAPABLE. Para obter mais informações, consulte a descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
 Se o driver não suportar transações, mas o aplicativo tiver a capacidade (usando uma API diferente do ODBC) de bloquear e desbloquear dados, os aplicativos podem obter suporte à transação bloqueando e desbloqueando registros e tabelas conforme necessário. Para implementar o exemplo de transferência de conta, o aplicativo bloquearia os registros de ambas as contas, copiaria os valores atuais, debitaria a primeira conta, creditaria a segunda conta e desbloquearia os registros. Se alguma etapa falhar, o aplicativo redefiniria as contas usando as cópias.  
  
 Mesmo as fontes de dados que suportam transações podem não ser capazes de suportar mais de uma transação por vez em um ambiente específico. Os aplicativos chamam **o SQLGetInfo** com a opção SQL_MULTIPLE_ACTIVE_TXN para determinar se uma fonte de dados pode suportar transações ativas simultâneas em mais de uma conexão no mesmo ambiente. Como há uma transação por conexão, isso só é interessante para aplicativos que têm múltiplas conexões com a mesma fonte de dados.
