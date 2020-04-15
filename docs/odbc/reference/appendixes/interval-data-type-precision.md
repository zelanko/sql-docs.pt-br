---
title: Precisão do tipo de dados de intervalo | Microsoft Docs
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
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290736"
---
# <a name="interval-data-type-precision"></a>Precisão do tipo de dados de intervalo
A precisão para um tipo de dados de intervalo inclui precisão de intervalo, precisão de intervalo e precisão de segundos.  
  
 O campo principal de um intervalo é um numérico assinado. O número máximo de dígitos para o campo líder é determinado por uma quantidade chamada *precisão líder de intervalo,* que é uma parte da declaração do tipo de dados. Por exemplo, a declaração: HORA DE INTERVALO(5) A MINUTO tem um intervalo de precisão de 5; o campo HORA pode levar valores de -99999 a 99999. A precisão de chumbo do intervalo está contida no campo SQL_DESC_DATETIME_INTERVAL_PRECISION do registro do descritor.  
  
 A lista de campos dos campos que um tipo de dados de intervalo é composta é chamada *de precisão de intervalo*. Não é um valor numérico, como o termo "precisão" pode implicar. Por exemplo, a precisão de intervalo do tipo INTERVAL DAY TO SECOND é a lista DIA, HORA, MINUTO, SEGUNDO. Não há campo descritor que detenha esse valor; a precisão do intervalo pode ser sempre determinada pelo tipo de dados de intervalo.  
  
 Qualquer tipo de dados de intervalo que tenha um campo SEGUNDO tem uma *precisão de segundos*. Este é o número de dígitos decimais permitidos na parte fracionada do valor dos segundos. Isto é diferente de outros tipos de dados, onde a precisão indica o número de dígitos antes do ponto decimal. A precisão de segundos de um tipo de dados de intervalo é o número de dígitos após o ponto decimal. Por exemplo, se a precisão de segundos for definida como 6, o número 123456 no campo de fração seria interpretado como 0,123456 e o número 1230 seria interpretado como 0,001230. Para outros tipos de dados, isso é referido como escala. A precisão dos segundos de intervalo está contida no campo SQL_DESC_PRECISION do descritor. Se a precisão do componente de segundos fracionados do valor do intervalo SQL for maior do que a que pode ser mantida na estrutura do intervalo C, é definido pelo driver se o valor de segundos fracionados no intervalo SQL é arredondado ou truncado quando convertido para a estrutura do intervalo C.  
  
 Quando o campo SQL_DESC_CONCISE_TYPE é definido como um tipo de dados de intervalo, o campo SQL_DESC_TYPE é definido como SQL_INTERVAL e o SQL_DESC_DATETIME_INTERVAL_CODE é definido como código para o tipo de dados de intervalo. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION é automaticamente definido para a precisão de 2 de intervalo padrão e o campo de SQL_DESC_PRECISION é automaticamente definido para a precisão de 6 segundos de intervalo padrão. Se qualquer um desses valores não for apropriado, o aplicativo deve definir explicitamente o campo descritor através de uma chamada para **SQLSetDescField**.
