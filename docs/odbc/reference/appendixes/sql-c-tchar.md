---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42afb911dda26cbda53f9cd14c883abb3775b94b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270532"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
O identificador de tipo SQL_C_TCHAR realmente não identificar um tipo de dados; é uma macro que existe dentro do arquivo de cabeçalho para conversão de Unicode. Ele é substituído por SQL_C_CHAR ou SQL_C_WCHAR dependendo da configuração do UNICODE **#define**. É útil para um aplicativo transferir dados de caractere que são compilados como um ANSI e um aplicativo Unicode.
