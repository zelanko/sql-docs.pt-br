---
description: Precisão do tipo de dados de intervalo
title: Precisão de tipo de dados de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 138cb4cae21b1c1fc0fd742cefac1b6f3a3e5978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483269"
---
# <a name="interval-data-type-precision"></a>Precisão do tipo de dados de intervalo
A precisão para um tipo de dados de intervalo inclui precisão à esquerda do intervalo, precisão do intervalo e precisão de segundos.  
  
 O campo à esquerda de um intervalo é um número assinado. O número máximo de dígitos para o campo principal é determinado por uma quantidade chamada *precisão inicial de intervalo,* que é uma parte da declaração de tipo de dados. Por exemplo, a declaração: intervalo de horas (5) a minuto tem uma precisão à esquerda de intervalo de 5; o campo de hora pode ter valores de-99999 a 99999. A precisão à esquerda do intervalo está contida no campo SQL_DESC_DATETIME_INTERVAL_PRECISION do registro do descritor.  
  
 A lista de campos dos quais um tipo de dados de intervalo é composto é chamada de *precisão de intervalo*. Ele não é um valor numérico, pois o termo "precisão" pode implicar. Por exemplo, a precisão de intervalo do tipo intervalo dia para segundo é a lista dia, hora, minuto, segundo. Não há nenhum campo de descritor que contenha esse valor; a precisão do intervalo sempre pode ser determinada pelo tipo de dados Interval.  
  
 Qualquer tipo de dados de intervalo que tenha um segundo campo tem uma *precisão de segundos*. Este é o número de dígitos decimais permitidos na parte fracionária do valor de segundos. Isso é diferente de para outros tipos de dados, em que precisão indica o número de dígitos antes do ponto decimal. A precisão de segundos de um tipo de dados de intervalo é o número de dígitos após o ponto decimal. Por exemplo, se a precisão de segundos for definida como 6, o número 123456 no campo de fração será interpretado como. 123456 e o número 1230 será interpretado como. 001230. Para outros tipos de dados, isso é conhecido como escala. A precisão do intervalo em segundos está contida no campo SQL_DESC_PRECISION do descritor. Se a precisão do componente de segundos fracionários do valor de intervalo do SQL for maior do que o que pode ser mantido na estrutura do intervalo de C, ele será definido pelo driver se o valor de segundos fracionários no intervalo SQL for arredondado ou truncado quando convertido na estrutura de intervalo de C.  
  
 Quando o campo de SQL_DESC_CONCISE_TYPE é definido como um tipo de dados de intervalo, o campo SQL_DESC_TYPE é definido como SQL_INTERVAL e o SQL_DESC_DATETIME_INTERVAL_CODE é definido como o código para o tipo de dados de intervalo. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION é definido automaticamente como a precisão inicial do intervalo padrão de 2, e o campo SQL_DESC_PRECISION é definido automaticamente como a precisão padrão do intervalo em segundos de 6. Se um desses valores não for apropriado, o aplicativo deverá definir explicitamente o campo de descritor por meio de uma chamada para **SQLSetDescField**.
