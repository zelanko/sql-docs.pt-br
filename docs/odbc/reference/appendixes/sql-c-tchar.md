---
title: SQL_C_TCHAR | Microsoft Docs
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
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b518868f3b6e77f9351877d57dc97cfee01a2c67
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlctchar"></a>SQL_C_TCHAR
O identificador de tipo SQL_C_TCHAR, na verdade, não identificar um tipo de dados; é uma macro que existe dentro do arquivo de cabeçalho para a conversão de Unicode. Ele é substituído por SQL_C_CHAR ou SQL_C_WCHAR dependendo da configuração do UNICODE **#define**. É útil para um aplicativo de transferência de dados de caractere que são compilados como um aplicativo de Unicode e de ANSI.
