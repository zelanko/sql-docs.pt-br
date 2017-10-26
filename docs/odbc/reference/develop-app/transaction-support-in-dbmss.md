---
title: "Suporte a transações em DBMSs | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14c1519122484542b57e286c248c25c3fd6c0886
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-support-in-dbmss"></a>Suporte a transações em DBMSs
Alguns bancos de dados, especialmente desktop bancos de dados, como dBASE, Paradox e Btrieve, não dão suporte a transações. Até mesmo entre bancos de dados que oferecem suporte a transações, há variação em quais tipos de instruções SQL podem ser em uma transação. Para obter mais informações, consulte a opção SQL_TXN_CAPABLE o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.

