---
title: Modelo de cursor suportado (Visual FoxPro ODBC Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301122"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modelo de cursor com suporte (Driver ODBC do Visual FoxPro)
O Driver Visual FoxPro ODBC suporta cursores *de bloco* *(conjunto de linhas)* e *estáticos.* Os cursores estáticos são suportados para qualquer driver que esteja em conformidade com a conformidade oDBC nível 1. O driver não suporta cursores dinâmicos, orientados por chave ou mistos (conjunto de chaves e dinâmicos).  
  
 Seu aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção SQL_CURSOR_TYPE de SQL_CURSOR_FORWARD_ONLY (cursor de bloco) ou SQL_CURSOR_STATIC (cursor estático).  
  
> [!NOTE]  
>  Se você chamar **SQLSetStmtOption** com uma opção SQL_CURSOR_TYPE diferente de SQL_CURSOR_FORWARD_ONLY ou SQL_CURSOR_STATIC, a função retorna SQL_SUCCESS_WITH_INFO com um SQLSTATE de 01S02 (valor de opção alterado). O driver define todos os modos de cursor sem suporte para SQL_CURSOR_STATIC.  
  
 Para obter mais informações sobre os tipos de cursor e sobre **o SQLSetStmtOption,** consulte a [referência do programador ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursor em bloco  
 Um conjunto de resultados somente leitura retornado ao cliente, responsável pela manutenção do armazenamento dos dados.  
  
## <a name="static-cursor"></a>cursor estático  
 Um instantâneo de um conjunto de dados definido pela consulta. Os cursores estáticos não refletem alterações em tempo real dos dados subjacentes por outros usuários. O buffer de memória do cursor é mantido pela biblioteca do cursor ODBC, que permite rolagem para frente e para trás.  
  
## <a name="rowset"></a>conjunto de linhas  
 Blocos de dados armazenados em um cursor, representando linhas recuperadas de uma fonte de dados.
