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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298666"
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
