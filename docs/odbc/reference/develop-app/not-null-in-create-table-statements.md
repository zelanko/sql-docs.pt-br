---
title: NÃO nulo em instruções CREATE TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4147e560d953b97ecba2e707d354bb6bf2ead59b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254233"
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL em instruções CREATE TABLE
Alguns bancos de dados e especialmente da área de trabalho, não dão suporte a **NOT NULL** restrição de coluna na **CREATE TABLE** instruções. Para obter mais informações, consulte a opção de SQL_NON_NULLABLE_COLUMNS na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
