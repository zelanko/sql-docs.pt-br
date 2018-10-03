---
title: SQLGetTypeInfo (Driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90bfbe29fd011f8b62527854f0ca5a179d8f63cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813864"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁVEL por Byte, contador, Double, tipos de dados único, longa e curta. (A capacidade de LIKE pode ser obtida ao converter o valor em um caractere usando as funções de conversão canônico do ODBC, em seguida, executar a comparação).
