---
title: Suporte à transação em DBMSs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fed5ea04e15002d31e35e25fac405a729929be8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305688"
---
# <a name="transaction-support-in-dbmss"></a>Suporte à transação em DBMSs
Alguns bancos de dados, especialmente da área de trabalho bancos de dados, como, Paradox, dBASE e Btrieve, damos suporte a transações. Até mesmo entre bancos de dados que oferecem suporte a transações, não há variação nas quais os tipos de instruções SQL podem ser em uma transação. Para obter mais informações, consulte a opção de SQL_TXN_CAPABLE na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
