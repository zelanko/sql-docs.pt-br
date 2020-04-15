---
title: SQLExecDirect (driver Visual FoxPro ODBC) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298666"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível do núcleo  
  
 Executa uma nova [e preparável declaração SQL](../../odbc/microsoft/visual-foxpro-terminology.md). O driver Visual FoxPro ODBC usa os valores atuais das variáveis de marcador de parâmetro se houver algum parâmetro na declaração.  
  
 Para criar um comando em lote para enviar mais de uma declaração SQL por vez, use um ponto e vírgula (;) para separar cada declaração SQL no lote.  
  
 Se a sua tabela, exibição ou nomes de campo contiverem espaços, feche os nomes nas marcas de aspas traseiras. Por exemplo, se o seu banco de dados contiver uma tabela chamada Minha Tabela e o campo Meu Campo, indescisse cada elemento do identificador da seguinte forma:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obter mais informações, consulte [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) no *Programador ODBC*.
