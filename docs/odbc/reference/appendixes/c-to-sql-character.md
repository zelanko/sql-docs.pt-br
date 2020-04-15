---
title: 'C a SQL: Personagem | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292027"
---
# <a name="c-to-sql-character"></a>C para SQL: caractere
Os identificadores do tipo de dados ODBC C do caractere são:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados de caracteres C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Quando os dados do caractere C são convertidos em dados SQL Unicode, o comprimento dos dados do Unicode deve ser um número uniforme.  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de byte de dados <= Comprimento da coluna.<br /><br /> Comprimento de byte de dados > comprimento da coluna.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento do caractere dos dados <= Comprimento da coluna.<br /><br /> Comprimento do caractere dos dados > comprimento da coluna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Dados convertidos sem truncação<br /><br /> Dados convertidos com truncação de dígitos fracionados[e]<br /><br /> A conversão de dados resultaria em perda de dígitos inteiros (em oposição ao fracionado)[e]<br /><br /> O valor dos dados não é *um numérico-literal*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> O valor dos dados não é *um numérico-literal*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menos de 2, e não são iguais a 1<br /><br /> Os dados são inferiores ou superiores a 0 ou igual a 2<br /><br /> Os dados não são *numéricos-literais*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Comprimento dos dados do byte) / 2 <= comprimento do byte da coluna<br /><br /> (Comprimento de byte de dados) / 2 > comprimento de byte da coluna<br /><br /> O valor dos dados não é um valor hexadecimal|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|O valor dos dados é um *ODBC-date-literal válido*<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; porção de tempo é zero<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; porção de tempo não é zero[a]<br /><br /> O valor dos dados não é um *ODBC-date-literal* ou *ODBC-timestamp-literal*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|O valor dos dados é um *ODBC-time-literal válido*<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; porção de segundos fracionados é zero[b]<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; porção de segundos fracionados não é zero[b]<br /><br /> O valor dos dados não é um *ODBC-time-literal* ou *ODBC-timestamp-literal*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é um *ODBC-timestamp-literal*válido; porção fracional segundos não truncado<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; porção fracional segundos truncado<br /><br /> O valor dos dados é um *ODBC-date-literal*válido [c]<br /><br /> O valor dos dados é um *ODBC-time-literal*válido [d]<br /><br /> O valor dos dados não é um *ODBC-date-literal,* *ODBC-time-literal*ou *ODBC-timestamp-literal*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo SQL|O valor dos dados é um *valor de intervalo*válido; não ocorre truncação<br /><br /> O valor dos dados é um *valor de intervalo*válido; o valor em um dos campos é truncado<br /><br /> O valor dos dados não é um intervalo válido literal|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] A parte do tempo do carimbo de tempo é truncada.  
  
 [b] A parte da data do carimbo de data é ignorada.  
  
 [c] A parte de tempo do carimbo de tempo é definida como zero.  
  
 [d] A parte da data do carimbo de data é definida para a data atual.  
  
 [e] A fonte driver/data espera efetivamente até que toda a seqüência tenha sido recebida (mesmo que os dados de caracteres sejam enviados em pedaços por chamadas para **SQLPutData**) antes de tentar realizar a conversão.  
  
 Quando os dados do caractere C são convertidos em dados SQL numéricos, data, hora ou carimbo de tempo, os espaços em branco de liderança e de arrasto são ignorados.  
  
 Quando os dados do caractere C são convertidos em dados SQL binários, cada dois bytes de dados de caracteres são convertidos em um único byte (8 bits) de dados binários. Cada dois bytes de dados de caracteres representam um número em forma hexadecimal. Por exemplo, "01" é convertido em um binário 00000001 e "FF" é convertido em um binário 11111111.  
  
 O driver sempre converte pares de dígitos hexadecimais em bytes individuais e ignora o byte de rescisão nula. Por causa disso, se o comprimento da seqüência de caracteres for estranho, o último byte da string (excluindo o byte de rescisão nula, se houver) não será convertido.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desencorajados de vincular dados de caractere C a um tipo de dados SQL binário. Esta conversão é geralmente ineficiente e lenta.
