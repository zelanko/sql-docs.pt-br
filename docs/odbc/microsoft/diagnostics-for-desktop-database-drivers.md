---
description: Diagnóstico para drivers de banco de dados de área de trabalho
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb5e4233ae77979df7b4b76ea845634fd7fd6ded
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471588"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico para drivers de banco de dados de área de trabalho
Todos os erros e avisos não verificados ou parcialmente verificados pelo Gerenciador de driver são tratados pelo driver. O driver também mapeia erros nativos, ou erros retornados pela fonte de dados, para sqlstates. Cada função listada na *referência do programador de ODBC* contém uma seção "diagnóstico" que especifica as condições e as mensagens.  
  
 Os aplicativos chamam **SQLGetDiagRec** para recuperar SQLSTATE, código de erro nativo e mensagens de diagnóstico. Chamar **SQLGetDiagField** e especificar o campo recupera campos de diagnóstico individuais. O nível de suporte dos identificadores de diagnóstico está listado na tabela a seguir.  
  
|DiagIdentifiers|Nível de suporte|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Sem suporte|  
|SQL_DIAG_CLASS_ORIGIN|Com suporte. Sempre "ODBC 3,0" para as versões 3,0 e posteriores deste driver.|  
|SQL_DIAG_COLUMN_NUMBER|Com suporte|  
|SQL_DIAG_CURSOR_ROW_COUNT|Sem suporte|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Sem suporte|  
|SQL_DIAG_MESSAGE_TEXT|Com suporte|  
|SQL_DIAG_NATIVE|Com suporte|  
|SQL_DIAG_NUMBER|Com suporte|  
|SQL_DIAG_RETURNCODE|Com suporte, mas implementado pelo Gerenciador de driver|  
|SQL_DIAG_ROW_COUNT|Com suporte|  
|SQL_DIAG_ROW_NUMBER|Com suporte|  
|SQL_DIAG_SERVER_NAME|Sem suporte|  
|SQL_DIAG_SQLSTATE|Com suporte|  
|SQL_DIAG_SUBCLASS_ORIGIN|Com suporte|
