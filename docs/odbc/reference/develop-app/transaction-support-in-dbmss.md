---
title: "Suporte a transações em DBMSs | Microsoft Docs"
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5785d2df5e9b1a3dccef92b8cf3e7996e88e6056
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="transaction-support-in-dbmss"></a>Suporte a transações em DBMSs
Alguns bancos de dados, especialmente desktop bancos de dados, como dBASE, Paradox e Btrieve, não dão suporte a transações. Até mesmo entre bancos de dados que oferecem suporte a transações, há variação em quais tipos de instruções SQL podem ser em uma transação. Para obter mais informações, consulte a opção SQL_TXN_CAPABLE o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
