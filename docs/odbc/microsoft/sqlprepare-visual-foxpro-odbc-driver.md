---
title: SQLPrepare (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42eabe40eb5324cf82c543525ce286dadc2a510a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
