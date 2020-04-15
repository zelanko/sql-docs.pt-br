---
title: Colunas Especiais SQL (Driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b439674c8bda3494b4cefd0c1118602b537cd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299376"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Recupera o conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.  
  
 O Driver Visual FoxPro ODBC retorna as colunas que compõem a chave principal na tabela FoxPro. (Veja [sqlprimarykeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) Se chamado com *fColType* definido para SQL_ROWVER, nenhuma coluna será devolvida. **SQLSpecialColumns** funciona apenas para fontes de dados que são [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obter mais informações, consulte [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) no *Programador ODBC ..*
