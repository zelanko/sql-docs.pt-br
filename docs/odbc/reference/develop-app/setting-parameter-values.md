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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66811d2364db546c3bddd787c1e0794f936f97c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445948"
---
# <a name="setting-parameter-values"></a>Configurar valores de parâmetro
Para definir o valor de um parâmetro, o aplicativo simplesmente define o valor da variável associada ao parâmetro. Não é importante quando esse valor é definido, desde que ele é definido antes da instrução é executada. O aplicativo pode definir o valor antes ou depois da associação da variável, e ele pode alterar o valor tantas vezes quanto desejar. Quando a instrução é executada, o driver simplesmente recupera o valor atual da variável. Isso é particularmente útil quando uma instrução preparada é executada mais de uma vez. o aplicativo define novos valores para algumas ou todas as variáveis de cada vez que a instrução é executada. Para obter um exemplo disso, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md), anteriormente nesta seção.  
  
 Se um buffer de comprimento/indicador foi associado na chamada para **SQLBindParameter**, ele deve ser definido como um dos valores a seguir antes da instrução for executada:  
  
-   O comprimento de bytes dos dados na variável associada. O driver verifica esse comprimento somente se a variável é o caractere ou binário (*ValueType* é SQL_C_CHAR ou SQL_C_BINARY).  
  
-   SQL_NTS. Os dados são uma cadeia de caracteres terminada em nulo.  
  
-   SQL_NULL_DATA. O valor de dados for NULL, e o driver ignora o valor da variável associada.  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC ou SQL_DATA_AT_EXEC. O valor do parâmetro é para ser enviada com **SQLPutData**. Para obter mais informações, consulte [enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md), mais adiante nesta seção.  
  
 A tabela a seguir mostra os valores da variável associada e o buffer de comprimento/indicador que o aplicativo define para uma variedade de valores de parâmetro.  
  
|Parâmetro<br /><br /> value|Parâmetro<br /><br /> (SQL)<br /><br /> tipo de dados|Variable (C)<br /><br /> tipo de dados|Valor em<br /><br /> associado<br /><br /> variável|Valor em<br /><br /> comprimento/indicador<br /><br /> buffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS or 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS or 2|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0[b]|--|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_CHAR|{t '13:00:00'}\0[a], [c]|SQL_NTS or 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" representa um caractere de finalização null. O caractere nulo de terminação é necessário somente se o valor no buffer de comprimento/indicador é SQL_NTS.  
  
 [b] os números nesta lista são os números armazenados nos campos da estrutura TIME_STRUCT.  
  
 [c] a cadeia de caracteres usa a cláusula de escape de data do ODBC. Para obter mais informações, consulte [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] drivers sempre devem verificar esse valor para ver se ele é um valor especial, como SQL_NULL_DATA.  
  
 O que um driver faz com um valor de parâmetro em tempo de execução é dependente do driver. Se necessário, o driver converte o valor do comprimento C de tipo e bytes de dados da variável associada para o tipo de dados SQL, precisão e escala do parâmetro. Na maioria dos casos, o driver, em seguida, envia o valor para a fonte de dados. Em alguns casos, ele formata o valor como texto e o insere na instrução SQL antes de enviar a instrução para a fonte de dados.
