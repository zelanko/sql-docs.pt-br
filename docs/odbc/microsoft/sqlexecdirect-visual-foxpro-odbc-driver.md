---
title: SQLExecDirect (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e701340217a885fbf1e3372c33ed1a8cfdb21457
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053853"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível de núcleo  
  
 Executa um novo [instrução de SQL preparável](../../odbc/microsoft/visual-foxpro-terminology.md). O Driver de ODBC do Visual FoxPro usa os valores atuais das variáveis de marcador de parâmetro se há quaisquer parâmetros na instrução.  
  
 Para criar um comando em lotes para enviar mais de uma instrução SQL por vez, use um ponto e vírgula (;) para separar cada instrução SQL no lote.  
  
 Se sua tabela, exibição ou nomes de campo contiverem espaços, coloque os nomes de aspas em volta marcas. Por exemplo, se seu banco de dados contiver uma tabela denominada My Table e o campo Meu campo, coloque cada elemento do identificador da seguinte maneira:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obter mais informações, consulte [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) na *referência do programador de ODBC*.
