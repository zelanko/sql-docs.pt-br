---
title: SqlGetTypeInfo (Driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64befe30be9ed7988e0c9348e9335eb632dd975c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295066"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do Excel Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE serão devolvidos na coluna SEARCHABLE para os tipos de dados Byte, Counter, Double, Single, Long e Short. (A capacidade LIKE pode ser alcançada convertendo o valor em um caractere usando as funções de conversão canônica oDBC e, em seguida, realizando a comparação.)  
  
 Quando o driver microsoft excel é usado, os nomes do tipo ODBC são retornados na coluna TYPE_NAME que é devolvida pelo **SQLGetTypeInfo**.
