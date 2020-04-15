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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299826"
---
# <a name="setting-parameter-values"></a>Configurar valores de parâmetro
Para definir o valor de um parâmetro, o aplicativo simplesmente define o valor da variável vinculada ao parâmetro. Não é importante quando esse valor é definido, desde que seja definido antes da declaração ser executada. O aplicativo pode definir o valor antes ou depois de vincular a variável, e pode alterar o valor quantas vezes quiser. Quando a declaração é executada, o driver simplesmente recupera o valor atual da variável. Isso é particularmente útil quando uma declaração preparada é executada mais de uma vez; o aplicativo define novos valores para algumas ou todas as variáveis cada vez que a declaração é executada. Para um exemplo disso, consulte [Execução Preparada,](../../../odbc/reference/develop-app/prepared-execution-odbc.md)anteriormente nesta seção.  
  
 Se um buffer de comprimento/indicador estiver vinculado na chamada para **SQLBindParameter,** ele deve ser definido como um dos seguintes valores antes da execução da declaração:  
  
-   O comprimento do byte dos dados na variável vinculada. O driver verifica este comprimento somente se a variável for de caráter ou binário *(ValueType* é SQL_C_CHAR ou SQL_C_BINARY).  
  
-   SQL_NTS. Os dados são uma seqüência de terminadas por nulo.  
  
-   Sql_null_data. O valor dos dados é NULL, e o driver ignora o valor da variável vinculada.  
  
-   SQL_DATA_AT_EXEC ou o resultado da SQL_LEN_DATA_AT_EXEC macro. O valor do parâmetro deve ser enviado com **SQLPutData**. Para obter mais informações, consulte [Enviar dados longos,](../../../odbc/reference/develop-app/sending-long-data.md)mais tarde nesta seção.  
  
 A tabela a seguir mostra os valores da variável vinculada e o buffer de comprimento/indicador que a aplicação define para uma variedade de valores de parâmetros.  
  
|Parâmetro<br /><br /> value|Parâmetro<br /><br /> (SQL)<br /><br /> tipo de dados|Variável (C)<br /><br /> tipo de dados|Valor em <br /><br /> associado<br /><br /> variável|Valor em <br /><br /> comprimento/indicador<br /><br /> buffer[d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS ou 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS ou 2|  
|Às 13h.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0[b]|--|  
|Às 13h.|SQL_TYPE_TIME|SQL_C_CHAR|{t '13:00:00'}\0[a], [c]|SQL_NTS ou 14|  
|NULO|SQL_SMALLINT|SQL_C_SSHORT|--|Sql_null_data|  
  
 [a] "\0" representa um caractere de rescisão nula. O caractere de rescisão nula é necessário apenas se o valor no buffer comprimento/indicador for SQL_NTS.  
  
 [b] Os números desta lista são os números armazenados nos campos da estrutura TIME_STRUCT.  
  
 [c] A string usa a cláusula de escape de data ODBC. Para obter mais informações, consulte [Data, Hora e Carimbo de Data](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] Os motoristas devem sempre verificar este valor para ver se é um valor especial, como SQL_NULL_DATA.  
  
 O que um motorista faz com um valor de parâmetro no tempo de execução é dependente do motorista. Se necessário, o driver converte o valor do tipo de dados C e o comprimento do byte da variável vinculada ao tipo de dados SQL, precisão e escala do parâmetro. Na maioria dos casos, o driver envia o valor para a fonte de dados. Em alguns casos, ele formatar o valor como texto e insere-o na instrução SQL antes de enviar a instrução para a fonte de dados.
