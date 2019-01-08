---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8df4339ae30b9058e5a5864c37807c6b02e4fdd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532116"
---
# <a name="interval-data-type-precision"></a>Precisão do tipo de dados de intervalo
Precisão para um tipo de dados de intervalo inclui o intervalo à esquerda de precisão, a precisão de intervalo e a precisão de segundos.  
  
 O campo à esquerda de um intervalo é um sinal numérico. O número máximo de dígitos para o campo à esquerda é determinado por uma quantidade chamada *intervalo à esquerda de precisão,* que é uma parte da declaração de tipo de dados. Por exemplo, a declaração: INTERVALO HOUR(5) para minuto tem uma precisão à esquerda do intervalo de 5; o campo de hora pode assumir valores de-99999 99999. O intervalo de precisão inicial está contido no campo SQL_DESC_DATETIME_INTERVAL_PRECISION do registro do descritor.  
  
 A lista de campos que um tipo de dados de intervalo é composto de é chamada *precisão de intervalo*. Não é um valor numérico, como o termo "precisão" implicar. Por exemplo, a precisão de intervalo do tipo INTERVAL DAY TO segundo é a lista dia, hora, minuto, segundo. Não há nenhum campo de descritor que contém esse valor; a precisão de intervalo sempre pode ser determinada pelo tipo de dados de intervalo.  
  
 Qualquer tipo de dados de intervalo que tem um segundo campo tem um *precisão de segundos*. Isso é o número de dígitos decimais permitido na parte fracionária do valor de segundos. Isso é diferente de outros tipos de dados, em que a precisão indica o número de dígitos antes do ponto decimal. A precisão de segundos de um tipo de dados de intervalo é o número de dígitos após o ponto decimal. Por exemplo, se a precisão de segundos é definida como 6, o número 123456 no campo de fração será interpretado como.123456 e o número 1230 poderia ser interpretados como.001230. Para outros tipos de dados, isso é chamado de escala. Precisão de segundos de intervalo está contida no campo do descritor de SQL_DESC_PRECISION. Se a precisão do componente de segundos fracionários do valor do intervalo SQL for maior que o que pode ser mantido na estrutura de intervalo de C, ele é definido pelo driver se o valor de segundos fracionários no intervalo de SQL é arredondado ou truncado quando convertidos para o C estrutura de intervalo.  
  
 Quando o campo SQL_DESC_CONCISE_TYPE é definido como um tipo de dados de intervalo, o campo SQL_DESC_TYPE for definido como SQL_INTERVAL e o SQL_DESC_DATETIME_INTERVAL_CODE é definido como o código para o tipo de dados de intervalo. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION é definido automaticamente para a precisão à esquerda do intervalo padrão de 2 e o campo SQL_DESC_PRECISION é definido automaticamente como a precisão de segundos de intervalo padrão de 6. Se qualquer um desses valores não é apropriado, o aplicativo deve definir explicitamente por meio de uma chamada para o campo do descritor **SQLSetDescField**.
