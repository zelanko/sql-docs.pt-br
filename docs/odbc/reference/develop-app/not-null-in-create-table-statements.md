---
title: "NÃO nulo nas instruções CREATE TABLE | Microsoft Docs"
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f48cae55d5147c0099599ab6e76bf11fe9e7597
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL nas instruções de tabela de criação
Alguns bancos de dados e especialmente área de trabalho, não dão suporte a **não NULL** restrição de coluna no **CREATE TABLE** instruções. Para obter mais informações, consulte a opção SQL_NON_NULLABLE_COLUMNS o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
