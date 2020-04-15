---
title: Diagnósticos para drivers de banco de dados de desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303477"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico para drivers de banco de dados de área de trabalho
Todos os erros e avisos não verificados ou parcialmente verificados pelo Driver Manager são tratados pelo motorista. O driver também mapeia erros nativos ou erros retornados pela fonte de dados para SQLSTATEs. Cada função listada na *Referência do Programador ODBC* contém uma seção "Diagnósticos" que especifica condições e mensagens.  
  
 Os aplicativos chamam **o SQLGetDiagRec** para recuperar sqlstate, código de erro nativo e mensagens de diagnóstico. Chamar **sqlGetDiagField** e especificar o campo recupera campos de diagnóstico individuais. O nível de suporte dos identificadores de diagnóstico está listado na tabela a seguir.  
  
|Identificadores diag|Nível de suporte|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Sem suporte|  
|SQL_DIAG_CLASS_ORIGIN| Com suporte. Sempre "ODBC 3.0" para as versões 3.0 e posteriores deste driver.|  
|SQL_DIAG_COLUMN_NUMBER|Com suporte|  
|SQL_DIAG_CURSOR_ROW_COUNT|Sem suporte|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Sem suporte|  
|SQL_DIAG_MESSAGE_TEXT|Com suporte|  
|SQL_DIAG_NATIVE|Com suporte|  
|SQL_DIAG_NUMBER|Com suporte|  
|SQL_DIAG_RETURNCODE|Suportado, mas implementado pelo Driver Manager|  
|SQL_DIAG_ROW_COUNT|Com suporte|  
|SQL_DIAG_ROW_NUMBER|Com suporte|  
|SQL_DIAG_SERVER_NAME|Sem suporte|  
|SQL_DIAG_SQLSTATE|Com suporte|  
|SQL_DIAG_SUBCLASS_ORIGIN|Com suporte|
