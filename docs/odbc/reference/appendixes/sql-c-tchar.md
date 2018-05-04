---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f2367dcae307e3152005c1bb47885a274c6cc0a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
O identificador de tipo SQL_C_TCHAR, na verdade, não identificar um tipo de dados; é uma macro que existe dentro do arquivo de cabeçalho para a conversão de Unicode. Ele é substituído por SQL_C_CHAR ou SQL_C_WCHAR dependendo da configuração do UNICODE **#define**. É útil para um aplicativo de transferência de dados de caractere que são compilados como um aplicativo de Unicode e de ANSI.
