---
title: "Suporte a transações | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4964565ce7de30b30fa3dc4c7705c5656ebcb88b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="transaction-support"></a>Suporte a transações
O grau de suporte para transações é definido pelo driver. ODBC foi projetado para ser implementada em um banco de dados usuário único ou de área de trabalho que não precisa gerenciar as várias atualizações para seus dados. Além disso, alguns bancos de dados que oferecem suporte a transações fazer apenas para as instruções de linguagem de manipulação de dados (DML) do SQL; há restrições ou semântica de transação especial em relação ao uso de Data Definition Language (DDL) quando uma transação está ativa. Ou seja, pode haver suporte a transações para várias atualizações simultâneas em tabelas, mas não para alterar o número e a definição das tabelas durante uma transação.  
  
 Um aplicativo determina se há suporte para transações, se DDL pode ser incluída em uma transação e efeitos especiais de inclusão de DDL em uma transação chamando **SQLGetInfo** com a opção SQL_TXN_CAPABLE. Para obter mais informações, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.  
  
 Se o driver não oferece suporte a transações, mas o aplicativo tem a capacidade de (usando uma API que não sejam ODBC) para bloquear e desbloquear dados, aplicativos podem obter suporte a transações, bloqueando e desbloqueando registros e tabelas conforme necessário. Para implementar o exemplo de transferência de conta, o aplicativo seria bloquear os registros de ambas as contas, copie os valores atuais, débito a primeira conta, a segunda conta de crédito e desbloquear os registros. Se todas as etapas de falharam, o aplicativo deve redefinir as contas usando as cópias.  
  
 Fontes de dados mesmo que oferecem suporte a transações podem não ser capazes de dar suporte a mais de uma transação de cada vez dentro de um ambiente específico. Aplicativos chamam **SQLGetInfo** com a opção SQL_MULTIPLE_ACTIVE_TXN para determinar se uma fonte de dados pode dar suporte a transações ativas simultâneas em mais de uma conexão no mesmo ambiente. Como há uma transação por conexão, isso só é interessante para aplicativos que têm várias conexões com a mesma fonte de dados.
