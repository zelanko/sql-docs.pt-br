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
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808927"
---
# <a name="transaction-support"></a>Suporte à transação
O grau de suporte para transações é definido pelo driver. ODBC é projetada para ser implementada em um banco de dados da área de trabalho ou de usuário único que não precisa gerenciar várias atualizações para seus dados. Além disso, alguns bancos de dados que oferecem suporte a transações fazer apenas para as instruções de linguagem de manipulação de dados (DML) do SQL; há restrições ou semântica de transação especial sobre o uso de linguagem de definição de dados (DDL) quando uma transação está ativa. Ou seja, pode haver suporte a transações para várias atualizações simultâneas em tabelas, mas não para alterar o número e a definição das tabelas durante uma transação.  
  
 Um aplicativo determina se há suporte para transações, se o DDL pode ser incluída em uma transação e qualquer efeitos especiais de inclusão de DDL em uma transação, chamando **SQLGetInfo** com a opção SQL_TXN_CAPABLE. Para obter mais informações, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.  
  
 Se o driver não oferece suporte a transações, mas o aplicativo tem a capacidade (usando uma API que não sejam ODBC) para bloquear e desbloquear os dados, aplicativos podem atingir o suporte a transações, bloqueando e desbloqueando registros e tabelas conforme necessário. Para implementar o exemplo de transferência de conta, o aplicativo seria bloquear os registros para ambas as contas, copie os valores atuais, a primeira conta de débito, a segunda conta de crédito e desbloquear os registros. Se todas as etapas falhar, o aplicativo seria redefinir as contas usando as cópias.  
  
 Fontes de dados, mesmo que oferecem suporte a transações podem não ser capazes de dar suporte a mais de uma transação por vez em um ambiente específico. Aplicativos chamam **SQLGetInfo** com a opção SQL_MULTIPLE_ACTIVE_TXN para determinar se uma fonte de dados pode dar suporte a transações ativas simultâneas em mais de uma conexão no mesmo ambiente. Como há uma transação por conexão, isso só é interessante para aplicativos que têm várias conexões para a mesma fonte de dados.
