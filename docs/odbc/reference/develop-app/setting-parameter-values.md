---
title: Definindo valores de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299826"
---
# <a name="setting-parameter-values"></a>Configurar valores de parâmetro
Para definir o valor de um parâmetro, o aplicativo simplesmente define o valor da variável associada ao parâmetro. Não é importante quando esse valor é definido, desde que ele seja definido antes que a instrução seja executada. O aplicativo pode definir o valor antes ou depois da vinculação da variável e pode alterar o valor quantas vezes desejar. Quando a instrução é executada, o driver simplesmente recupera o valor atual da variável. Isso é particularmente útil quando uma instrução preparada é executada mais de uma vez; o aplicativo define novos valores para algumas ou todas as variáveis sempre que a instrução é executada. Para obter um exemplo disso, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md), anteriormente nesta seção.  
  
 Se um buffer de comprimento/indicador tiver sido associado na chamada para **SQLBindParameter**, ele deverá ser definido como um dos valores a seguir antes que a instrução seja executada:  
  
-   O comprimento de bytes dos dados na variável associada. O driver verifica esse comprimento somente se a variável for Character ou binary (*ValueType* é SQL_C_CHAR ou SQL_C_BINARY).  
  
-   SQL_NTS. Os dados são uma cadeia de caracteres terminada em nulo.  
  
-   SQL_NULL_DATA. O valor de dados é nulo e o driver ignora o valor da variável associada.  
  
-   SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. O valor do parâmetro deve ser enviado com **SQLPutData**. Para obter mais informações, consulte [enviando dados longos](../../../odbc/reference/develop-app/sending-long-data.md), mais adiante nesta seção.  
  
 A tabela a seguir mostra os valores da variável associada e o buffer de comprimento/indicador que o aplicativo define para uma variedade de valores de parâmetro.  
  
|Parâmetro<br /><br /> value|Parâmetro<br /><br /> SQL<br /><br /> tipo de dados|Variável (C)<br /><br /> tipo de dados|Valor em <br /><br /> associado<br /><br /> variável|Valor em <br /><br /> comprimento/indicador<br /><br /> buffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS ou 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS ou 2|  
|13:00|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13, 0, 0 [b]|--|  
|13:00|SQL_TYPE_TIME|SQL_C_CHAR|{T' 13:00:00 '} \ 0 [a], [c]|SQL_NTS ou 14|  
|NULO|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0" representa um caractere de terminação nula. O caractere de terminação nula será necessário somente se o valor no buffer de comprimento/indicador for SQL_NTS.  
  
 [b] os números nessa lista são os números armazenados nos campos da estrutura de TIME_STRUCT.  
  
 [c] a cadeia de caracteres usa a cláusula ODBC Date escape. Para obter mais informações, consulte [data, hora e literais de carimbo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de hora.  
  
 [d] os drivers sempre devem verificar esse valor para ver se ele é um valor especial, como SQL_NULL_DATA.  
  
 O que um driver faz com um valor de parâmetro no momento da execução é dependente de driver. Se necessário, o driver converte o valor do tipo de dados C e o comprimento de bytes da variável associada para o tipo de dados SQL, a precisão e a escala do parâmetro. Na maioria dos casos, o driver envia o valor para a fonte de dados. Em alguns casos, ele formata o valor como texto e o insere na instrução SQL antes de enviar a instrução para a fonte de dados.
