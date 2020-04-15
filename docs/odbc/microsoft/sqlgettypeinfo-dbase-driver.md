---
title: SQLGetTypeInfo (driver dBASE) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 711652e22318d089b02fe8e79cb592f0a42dfff9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295126"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do dBASE Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE serão devolvidos na coluna SEARCHABLE para os tipos de dados Byte, Counter, Double, Single, Long e Short. (A capacidade LIKE pode ser alcançada convertendo o valor em um caractere usando as funções de conversão canônica oDBC e, em seguida, realizando a comparação.)
