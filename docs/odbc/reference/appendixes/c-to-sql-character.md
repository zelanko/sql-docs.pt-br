---
description: 'C para SQL: caractere'
title: 'C to SQL: caractere | Microsoft Docs'
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
ms.openlocfilehash: 0ab8f1c0471c6e079f792aa40119f13cb31ca9ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500019"
---
# <a name="c-to-sql-character"></a>C para SQL: caractere
Os identificadores para o tipo de dados ODBC C são:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados de caractere C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Quando os dados do caractere C são convertidos em dados SQL Unicode, o comprimento dos dados Unicode deve ser um número par.  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de bytes de dados <= comprimento da coluna.<br /><br /> Comprimento de bytes de comprimento de coluna de > de dados.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caracteres de <de dados = comprimento da coluna.<br /><br /> Comprimento de caracteres de data > comprimento da coluna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Dados convertidos sem truncamento<br /><br /> Dados convertidos com truncamento de dígitos fracionários [e]<br /><br /> A conversão de dados resultaria em perda de inteiros (em oposição aos dígitos fracionários) [e]<br /><br /> O valor dos dados não é um *literal numérico*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> O valor dos dados não é um *literal numérico*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menores que 2 e não iguais a 1<br /><br /> Os dados são menores que 0 ou maiores ou iguais a 2<br /><br /> Os dados não são um *literal numérico*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Comprimento de bytes de dados)/2 <= comprimento de byte de coluna<br /><br /> (Comprimento de bytes de dados)/2 > comprimento de byte de coluna<br /><br /> O valor dos dados não é um valor hexadecimal|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|O valor dos dados é um *ODBC-Date-literal* válido<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; a parte de hora é zero<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; a parte de hora é diferente de zero [a]<br /><br /> O valor dos dados não é um *ODBC-Date-literal* ou *ODBC-timestamp-literal* válido|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|O valor dos dados é um *ODBC-time-literal* válido<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; a parte de segundos fracionários é zero [b]<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; a parte de segundos fracionários é diferente de zero [b]<br /><br /> O valor dos dados não é um *tempo de ODBC* -literal ou *ODBC-timestamp-literal* válido|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é um *ODBC-timestamp-literal*válido; parte de segundos fracionários não truncada<br /><br /> O valor dos dados é um *ODBC-timestamp-literal*válido; parte de segundos fracionários truncada<br /><br /> O valor dos dados é um *ODBC-Date-literal*válido [c]<br /><br /> O valor dos dados é um *ODBC-time-literal*válido [d]<br /><br /> O valor dos dados não é um *ODBC-Date-literal*, *ODBC-time-literal*ou *ODBC-timestamp-literal*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo SQL|O valor dos dados é um *valor de intervalo*válido; nenhum truncamento ocorre<br /><br /> O valor dos dados é um *valor de intervalo*válido; o valor em um dos campos está truncado<br /><br /> O valor dos dados não é um literal de intervalo válido|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] a parte de tempo do carimbo de data/hora está truncada.  
  
 [b] a parte de data do carimbo de hora é ignorada.  
  
 [c] a parte de tempo do carimbo de data/hora é definida como zero.  
  
 [d] a parte de data do carimbo de hora é definida como a data atual.  
  
 [e] a fonte de driver/dados aguarda efetivamente até que toda a cadeia de caracteres tenha sido recebida (mesmo que os dados de caracteres sejam enviados em partes por chamadas para **SQLPutData**) antes de tentar executar a conversão.  
  
 Quando os dados do caractere C são convertidos em dados numéricos, de data, hora ou timestamp, os espaços em branco à esquerda e à direita são ignorados.  
  
 Quando os dados do caractere C são convertidos em dados SQL binários, cada um dos dois bytes de dados de caractere são convertidos em um único byte (8 bits) de dados binários. Cada dois bytes de dados de caractere representam um número em formato hexadecimal. Por exemplo, "01" é convertido em um binário 00000001 e "FF" é convertido em um binário 11111111.  
  
 O driver sempre converte pares de dígitos hexadecimais em bytes individuais e ignora o byte de terminação nula. Por isso, se o comprimento da cadeia de caracteres for ímpar, o último byte da cadeia de caracteres (excluindo o byte de terminação nula, se houver) não será convertido.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desencorajados de vincular dados C de caracteres a um tipo de dados SQL binário. Normalmente, essa conversão é ineficiente e lenta.
