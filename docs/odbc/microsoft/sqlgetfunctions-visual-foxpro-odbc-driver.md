---
title: SQLGetFunctions (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da74bbb64a76f6c3ff6c55754798b975dab83826
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003327"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Retorna TRUE para todas as funções com suporte.  
  
 O driver ODBC do Visual FoxPro dá suporte a todas as funções de núcleo e nível 1 da API ODBC. A tabela a seguir indica se o driver dá suporte a uma função de nível 2 específica.  
  
|*Função*|Suportado|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|Não|  
|SQL_API_SQLCOLUMNPRIVELEGES|Não|  
|SQL_API_SQLDATASOURCES|Sim|  
|SQL_API_SQLDESCRIBEPARAM|Não|  
|SQL_API_SQLDRIVERS|Sim|  
|SQL_API_SQLEXTENDEDFETCH|Sim|  
|SQL_API_SQLFOREIGNKEYS|Não|  
|SQL_API_SQLMORERESULTS|Sim|  
|SQL_API_SQLNATIVESQL|Não|  
|SQL_API_SQLNUMPARAMS|Sim|  
|SQL_API_SQLPARAMOPTIONS|Sim|  
|SQL_API_SQLPRIMARYKEYS|Sim|  
|SQL_API_SQLPROCEDURECOLUMNS|Não|  
|SQL_API_SQLPROCEDURES|Não|  
|SQL_API_SQLSETPOS|Sim|  
|SQL_API_SQLSETSCROLLOPTIONS|Sim|  
|SQL_API_SQLTABLEPRIVILEGES|Não|  
  
 Para obter mais informações, consulte [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) na *referência do programador de ODBC*.
