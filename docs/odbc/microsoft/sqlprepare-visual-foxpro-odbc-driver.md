---
title: SQLPrepare (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 53b3631e1f5a1827e9ebd18e0ed1537d5772a5ee
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 ODBC API conformidade: Nível de núcleo  
  
 Prepara uma instrução SQL, como planejar a otimizar e execute a instrução. A instrução SQL é compilada para execução pelo [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Se sua tabela, exibição ou nomes de campo contiverem espaços, coloque os nomes em aspas marcas ('). Por exemplo, se seu banco de dados contém uma tabela chamada minha tabela e o campo Meu campo, coloque cada elemento do identificador da seguinte maneira:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Para obter mais informações, consulte [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) no *referência do programador de ODBC*.
