---
title: SQLExecDirect (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053853"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Executa uma nova [instrução SQL preparável](../../odbc/microsoft/visual-foxpro-terminology.md). O driver ODBC do Visual FoxPro usa os valores atuais das variáveis de marcador de parâmetro se existirem parâmetros na instrução.  
  
 Para criar um comando em lotes para enviar mais de uma instrução SQL por vez, use um ponto-e-vírgula (;) para separar cada instrução SQL no lote.  
  
 Se os nomes de tabela, exibição ou campo contiverem espaços, coloque os nomes nas aspas de fundo. Por exemplo, se seu banco de dados contiver uma tabela denominada minha tabela e o campo meu campo, coloque cada elemento do identificador da seguinte maneira:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obter mais informações, consulte [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) na *referência do programador de ODBC*.
