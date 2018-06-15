---
title: Drivers de banco de dados de diagnóstico para a área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d5d82eb22f57fd033ea9250e1dd5532e72174e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904221"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico para Drivers de banco de dados de área de trabalho
Todos os erros e avisos não verificadas ou parcialmente verificadas pelo Gerenciador de Driver são tratados pelo driver. O driver também mapeia nativo erros ou erros retornados pela fonte de dados, para SQLSTATEs. Cada função listada no *referência do programador de ODBC* contém uma seção de "Diagnóstico" que especifica as condições e mensagens.  
  
 Aplicativos chamam **SQLGetDiagRec** para recuperar o SQLSTATE, código de erro nativo e mensagens de diagnóstico. Chamando **SQLGetDiagField** e especificando o campo recupera os campos de diagnóstico individuais. O nível de suporte dos identificadores de diagnóstico é listado na tabela a seguir.  
  
|DiagIdentifiers|Nível de suporte|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Sem suporte|  
|SQL_DIAG_CLASS_ORIGIN|Tem suporte. Sempre "ODBC 3.0" para versões 3.0 e posterior deste driver.|  
|SQL_DIAG_COLUMN_NUMBER|Tem suporte|  
|SQL_DIAG_CURSOR_ROW_COUNT|Sem suporte|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Sem suporte|  
|SQL_DIAG_MESSAGE_TEXT|Tem suporte|  
|SQL_DIAG_NATIVE|Tem suporte|  
|SQL_DIAG_NUMBER|Tem suporte|  
|SQL_DIAG_RETURNCODE|Com suporte, mas implementado pelo Gerenciador de Driver|  
|SQL_DIAG_ROW_COUNT|Tem suporte|  
|SQL_DIAG_ROW_NUMBER|Tem suporte|  
|SQL_DIAG_SERVER_NAME|Sem suporte|  
|SQL_DIAG_SQLSTATE|Tem suporte|  
|SQL_DIAG_SUBCLASS_ORIGIN|Tem suporte|
