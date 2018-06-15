---
title: SQLExecDirect (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0086dc41e34ac543cf0cd560332454b0024de48e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902601"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 ODBC API conformidade: Nível de núcleo  
  
 Executa uma nova [preparável instrução de SQL](../../odbc/microsoft/visual-foxpro-terminology.md). O Driver de ODBC do Visual FoxPro usa os valores atuais das variáveis de marcador de parâmetro, se houver quaisquer parâmetros na instrução.  
  
 Para criar um comando em lotes para enviar mais de uma instrução SQL em um momento, use um ponto e vírgula (;) para separar cada instrução SQL no lote.  
  
 Se sua tabela, exibição ou nomes de campo contiverem espaços, coloque os nomes de aspas em marcas. Por exemplo, se seu banco de dados contém uma tabela chamada minha tabela e o campo Meu campo, coloque cada elemento do identificador da seguinte maneira:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obter mais informações, consulte [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) no *referência do programador de ODBC*.
