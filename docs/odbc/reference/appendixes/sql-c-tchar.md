---
title: SQL_C_TCHAR | Microsoft Docs
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
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cce7467dd03210d60fad060e25885baf0df38399
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909161"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
O identificador de tipo SQL_C_TCHAR, na verdade, não identificar um tipo de dados; é uma macro que existe dentro do arquivo de cabeçalho para a conversão de Unicode. Ele é substituído por SQL_C_CHAR ou SQL_C_WCHAR dependendo da configuração do UNICODE **#define**. É útil para um aplicativo de transferência de dados de caractere que são compilados como um aplicativo de Unicode e de ANSI.
