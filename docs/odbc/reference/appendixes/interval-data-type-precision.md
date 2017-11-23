---
title: "Precisão de tipo de dados de intervalo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba46b5cc82fd2ac36e9a3cf920b81bc48b0d9baa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-type-precision"></a>Precisão de tipo de dados de intervalo
Precisão para um tipo de dados de intervalo inclui intervalo à esquerda a precisão, a precisão do intervalo e a precisão de segundos.  
  
 O campo à esquerda de um intervalo é um numérico assinado. O número máximo de dígitos para o campo principal é determinado por uma quantidade chamada *intervalo à esquerda de precisão,* que é uma parte da declaração de tipo de dados. Por exemplo, a declaração: intervalo HOUR(5) para minuto tem um intervalo à esquerda a precisão de 5; o campo de hora pode assumir valores de –99999 e 99999. O intervalo de precisão principal está contido no campo SQL_DESC_DATETIME_INTERVAL_PRECISION de registro do descritor.  
  
 A lista de campos de um tipo de dados de intervalo é composto é chamada *precisão do intervalo*. Não é um valor numérico, como o termo "precisão" poderá indicar. Por exemplo, a precisão do intervalo do tipo de intervalo dia a segunda é lista dia, hora, minuto, segundo. Não há nenhum campo de descritor que contém esse valor; a precisão do intervalo sempre pode ser determinada pelo tipo de dados de intervalo.  
  
 Qualquer tipo de dados de intervalo que tem um segundo campo tem um *precisão em segundos*. Este é o número de dígitos permitido na parte fracionária do valor de segundos. Isso é diferente de outros tipos de dados, em que a precisão indica o número de dígitos antes do ponto decimal. A precisão de segundos de um tipo de dados de intervalo é o número de dígitos após o ponto decimal. Por exemplo, se a precisão de segundos é definida como 6, o número 123456 no campo de fração será interpretado como.123456 e o número 1230 serão interpretadas como.001230. Para outros tipos de dados, isso é conhecido como a escala. Precisão de segundos de intervalo está contida no campo SQL_DESC_PRECISION do descritor. Se a precisão do componente frações de segundos do valor de intervalo SQL for maior do que o que pode ser mantido na estrutura de intervalo de C, ele é definido pelo driver se o valor de segundos fracionários no intervalo de SQL é arredondado ou truncado quando convertidos para o C estrutura do intervalo.  
  
 Quando o campo SQL_DESC_CONCISE_TYPE é definido como um tipo de dados de intervalo, o campo SQL_DESC_TYPE é definido como SQL_INTERVAL e o SQL_DESC_DATETIME_INTERVAL_CODE é definido como o código para o tipo de dados de intervalo. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION é definido automaticamente como a precisão à esquerda do intervalo padrão de 2, e o campo SQL_DESC_PRECISION é definido automaticamente como a precisão de segundos de intervalo padrão de 6. Se qualquer um desses valores não é apropriado, o aplicativo deve definir explicitamente por meio de uma chamada para o campo do descritor **SQLSetDescField**.
