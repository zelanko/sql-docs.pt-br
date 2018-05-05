---
title: Suporte a transações em DBMSs | Microsoft Docs
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7095120f0a41bb4df5a3607c55abeb3a9da194f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support-in-dbmss"></a>Suporte a transações em DBMSs
Alguns bancos de dados, especialmente desktop bancos de dados, como dBASE, Paradox e Btrieve, não dão suporte a transações. Até mesmo entre bancos de dados que oferecem suporte a transações, há variação em quais tipos de instruções SQL podem ser em uma transação. Para obter mais informações, consulte a opção SQL_TXN_CAPABLE o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
