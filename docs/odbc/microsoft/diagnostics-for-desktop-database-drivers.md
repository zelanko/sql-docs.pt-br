---
title: Diagnóstico para drivers de banco de dados de desktop | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031225"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico para drivers de banco de dados de área de trabalho
Todos os erros e avisos não verificados ou parcialmente verificados pelo Gerenciador de driver são tratados pelo driver. O driver também mapeia erros nativos, ou erros retornados pela fonte de dados, para sqlstates. Cada função listada na *referência do programador de ODBC* contém uma seção "diagnóstico" que especifica as condições e as mensagens.  
  
 Os aplicativos chamam **SQLGetDiagRec** para recuperar SQLSTATE, código de erro nativo e mensagens de diagnóstico. Chamar **SQLGetDiagField** e especificar o campo recupera campos de diagnóstico individuais. O nível de suporte dos identificadores de diagnóstico está listado na tabela a seguir.  
  
|DiagIdentifiers|Nível de suporte|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Sem suporte|  
|SQL_DIAG_CLASS_ORIGIN| Com suporte. Sempre "ODBC 3,0" para as versões 3,0 e posteriores deste driver.|  
|SQL_DIAG_COLUMN_NUMBER|Suportado|  
|SQL_DIAG_CURSOR_ROW_COUNT|Sem suporte|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Sem suporte|  
|SQL_DIAG_MESSAGE_TEXT|Suportado|  
|SQL_DIAG_NATIVE|Suportado|  
|SQL_DIAG_NUMBER|Suportado|  
|SQL_DIAG_RETURNCODE|Com suporte, mas implementado pelo Gerenciador de driver|  
|SQL_DIAG_ROW_COUNT|Suportado|  
|SQL_DIAG_ROW_NUMBER|Suportado|  
|SQL_DIAG_SERVER_NAME|Sem suporte|  
|SQL_DIAG_SQLSTATE|Suportado|  
|SQL_DIAG_SUBCLASS_ORIGIN|Suportado|
