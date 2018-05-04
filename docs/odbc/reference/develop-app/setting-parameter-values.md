---
title: Definir valores de parâmetro | Microsoft Docs
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
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e41f775ef6640f4f82aa16cea038becc305bf5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-parameter-values"></a>Definir valores de parâmetro
Para definir o valor de um parâmetro, o aplicativo simplesmente define o valor da variável associada ao parâmetro. Não é importante quando esse valor for definido, desde que ele está definido antes da instrução é executada. O aplicativo pode definir o valor antes ou depois de associação da variável, e ele pode alterar o valor de quantas vezes desejar. Quando a instrução é executada, o driver simplesmente recupera o valor atual da variável. Isso é particularmente útil quando uma instrução preparada é executada mais de uma vez; o aplicativo define novos valores para algumas ou todas as variáveis de cada vez que a instrução é executada. Para obter um exemplo disso, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)anteriormente nesta seção.  
  
 Se um buffer de comprimento/indicador foi associado na chamada para **SQLBindParameter**, ele deve ser definido para um dos valores a seguir antes da instrução é executada:  
  
-   O comprimento de bytes dos dados na variável associada. O driver verifica esse comprimento somente se a variável for caractere ou binário (*ValueType* é SQL_C_CHAR ou SQL_C_BINARY).  
  
-   SQL_NTS. Os dados são uma cadeia de caracteres terminada em nulo.  
  
-   SQL_NULL_DATA. O valor dos dados for NULL, e o driver ignora o valor da variável associada.  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC ou SQL_DATA_AT_EXEC. O valor do parâmetro é para ser enviada com **SQLPutData**. Para obter mais informações, consulte [enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md), mais adiante nesta seção.  
  
 A tabela a seguir mostra os valores da variável associada e o buffer de comprimento/indicador que define o aplicativo para uma variedade de valores de parâmetro.  
  
|Parâmetro<br /><br /> value|Parâmetro<br /><br /> (SQL)<br /><br /> tipo de dados|Variable (C)<br /><br /> tipo de dados|Valor em<br /><br /> associado<br /><br /> variável|Valor em<br /><br /> comprimento/indicador<br /><br /> buffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS ou 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|SQL_NTS ou 2|  
|13.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|13.|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a], [c]|SQL_NTS ou 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" representa um caractere null de terminação. O caractere null de terminação é necessário somente se o valor no buffer de comprimento/indicador é SQL_NTS.  
  
 [b] o os números na lista são armazenados nos campos da estrutura de TIME_STRUCT.  
  
 [c] a cadeia de caracteres usa a cláusula de escape de data do ODBC. Para obter mais informações, consulte [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] drivers sempre devem verificar esse valor para ver se ele é um valor especial, como SQL_NULL_DATA.  
  
 O que faz um driver com um valor de parâmetro em tempo de execução é dependente do driver. Se necessário, o driver converte o valor do comprimento C de byte e tipo de dados da variável de associado para o tipo de dados SQL, precisão e escala do parâmetro. Na maioria dos casos, o driver envia o valor para a fonte de dados. Em alguns casos, ele formata o valor como texto e o insere na instrução SQL antes de enviar a instrução para a fonte de dados.
