---
title: Truncamento de dados (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e735659fb2898c2ab6bc428d7ad6fc0f5759f17c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117938"
---
# <a name="data-truncation-ssis"></a>Truncamento de dados (SSIS)
  Uma expressão pode fazer com que os dados sejam truncados inadvertidamente. O truncamento pode ocorrer nas seguintes circunstâncias:  
  
-   cadeias de caracteres. Por exemplo, a conversão de dados da cadeia de caracteres com um tipo de dados DT_WSTR para uma cadeia de caracteres com o mesmo comprimento, medido em caracteres, com um tipo de dados DT_STR causa perda de dados, se a cadeia de caracteres original contém caracteres de byte duplo.  
  
-   Dígitos significantes. Por exemplo, a conversão de um inteiro de um tipo de dados DT_I4 para um tipo de dados DT_I2 ou de um inteiro não assinado para um inteiro assinado.  
  
-   Dígitos insignificantes. Por exemplo, a conversão de um número real de DT_R8 para um DT_R4 ou de um inteiro de um tipo de dados DT_I4 para um tipo de dados DT_R4.  
  
 O avaliador de expressão identifica conversões explícitas que podem causar truncamento e emite um aviso quando a expressão é analisada. Por exemplo, o avaliador de expressão o advertirá se uma cadeia de 30 caracteres for convertida em uma cadeia de 20 caracteres.  
  
> [!NOTE]  
>  O truncamento não é verificado no tempo de execução; dados são truncados sem aviso. Porém, a maioria dos adaptadores e das transformações de dados aceita saídas de erro que podem controlar a disposição de linhas de erro. Para obter mais informações sobre truncamento de manipulação de dados, consulte [Error Handling in Data](../data-flow/error-handling-in-data.md).  
  
  