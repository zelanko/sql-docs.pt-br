---
description: Suporte à transação em DBMSs
title: Suporte a transações em DBMSs | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487449"
---
# <a name="transaction-support-in-dbmss"></a>Suporte à transação em DBMSs
Alguns bancos de dados, especialmente bancos de dados da área de trabalho, como dBASE, Paradox e Btrieve, não dão suporte a transações. Mesmo entre os bancos de dados que dão suporte a transações, há variação no que os tipos de instruções SQL podem estar em uma transação. Para obter mais informações, consulte a opção SQL_TXN_CAPABLE na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
