---
title: SQLPrepare (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14c9358d04e539eb2c77a00e195e8216cd0f5496
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301552"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Prepara uma instrução SQL planejando como otimizar e executar a instrução. A instrução SQL é compilada para execução por [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Se os nomes de tabela, exibição ou campo contiverem espaços, coloque os nomes nas marcas de aspas ('). Por exemplo, se seu banco de dados contiver uma tabela denominada minha tabela e o campo meu campo, coloque cada elemento do identificador da seguinte maneira:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Para obter mais informações, consulte [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) na *referência do programador de ODBC*.
