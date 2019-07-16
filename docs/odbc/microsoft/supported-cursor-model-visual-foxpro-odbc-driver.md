---
title: Suporte para o modelo de Cursor (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e623c0ce5135a4b2e558be9c405ec2757e605ceb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080710"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modelo de cursor com suporte (Driver ODBC do Visual FoxPro)
O Driver de ODBC do Visual FoxPro dá suporte a ambos *bloco* (*conjunto de linhas*) e *estático* cursores. Cursores estáticos são compatíveis com qualquer driver que está em conformidade com a conformidade de nível 1 ODBC. O driver não oferece suporte a dinâmicos, controlados por ou misto (conjunto de chaves e dinâmico) cursores.  
  
 O aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção de SQL_CURSOR_TYPE de SQL_CURSOR_FORWARD_ONLY (cursor em bloco) ou SQL_CURSOR_STATIC (cursor estático).  
  
> [!NOTE]  
>  Se você chamar **SQLSetStmtOption** com uma opção SQL_CURSOR_TYPE diferente SQL_CURSOR_FORWARD_ONLY ou SQL_CURSOR_STATIC, a função retorna SQL_SUCCESS_WITH_INFO com um SQLSTATE de 01S02 (valor de opção alterado). O driver define todos os modos de cursor sem suporte para SQL_CURSOR_STATIC.  
  
 Para obter mais informações sobre tipos de cursor e aproximadamente **SQLSetStmtOption**, consulte o [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursor em bloco  
 Um conjunto de resultados de rolagem de avanço, somente leitura retornado ao cliente, quem é responsável por manter o armazenamento de dados.  
  
## <a name="static-cursor"></a>cursor estático  
 Um instantâneo de um conjunto de dados definido pela consulta. Cursores estáticos não refletem as alterações em tempo real dos dados subjacentes por outros usuários. O buffer de memória do cursor é mantido pela biblioteca de cursores ODBC, que permite a rolagem para frente e para trás.  
  
## <a name="rowset"></a>conjunto de linhas  
 Blocos de dados armazenados em um cursor, que representa a linhas recuperadas da fonte de dados.
