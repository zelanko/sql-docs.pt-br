---
title: 'C para SQL: caractere | Microsoft Docs'
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
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d104581a54a16064eec791ad3419770b1538ff1e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-character"></a>C para SQL: caractere
Os identificadores para o caractere de tipo de dados ODBC C são:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de caractere C podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Quando os dados de caractere C são convertidos em dados Unicode SQL, o comprimento dos dados Unicode deve ser um número par.  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento em bytes de dados < = comprimento da coluna.<br /><br /> Comprimento em bytes de dados > tamanho da coluna.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento dos dados de caracteres < = comprimento da coluna.<br /><br /> Comprimento dos dados de caracteres > tamanho da coluna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Convertido sem truncamento de dados<br /><br /> Os dados convertidos com truncamento de dígitos fracionários [e]<br /><br /> Conversão de dados pode resultar em perda de dígitos de inteiro (em vez de frações) [e]<br /><br /> Valor de dados não é um *literal numérico*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Dados estão dentro do intervalo do tipo de dados ao qual o número é convertido<br /><br /> Dados estão fora do intervalo do tipo de dados ao qual o número é convertido<br /><br /> Valor de dados não é um *literal numérico*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Dados são 0 ou 1<br /><br /> Dados for maiores que 0, menor que 2 e não é igual a 1<br /><br /> Dados são menor que 0 ou maior que ou igual a 2<br /><br /> Dados não são um *literal numérico*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Comprimento em bytes de dados) / 2 < = comprimento de bytes da coluna<br /><br /> (Comprimento em bytes de dados) / 2 > bytes de coluna<br /><br /> Valor de dados não é um valor hexadecimal|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Valor de dados é uma opção válida *literal de data de ODBC*<br /><br /> Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; parte de hora for zero<br /><br /> Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; parte de hora é diferente de zero [a]<br /><br /> Valor de dados não é válido *literal de data de ODBC* ou *literal de carimbo de hora de ODBC*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Valor de dados é uma opção válida *literal de hora de ODBC*<br /><br /> Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; fracionários parte de segundos é zero [b]<br /><br /> Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; fracionários parte de segundos é diferente de zero [b]<br /><br /> Valor de dados não é válido *literal de hora de ODBC* ou *literal de carimbo de hora de ODBC*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; fracionários parte de segundos não truncado<br /><br /> Valor de dados é uma opção válida *literal de carimbo de hora de ODBC*; fracionários parte de segundos truncado<br /><br /> Valor de dados é uma opção válida *literal de data de ODBC*[c]<br /><br /> Valor de dados é uma opção válida *literal de hora de ODBC*[d]<br /><br /> Valor de dados não é válido *literal de data de ODBC*, *literal de hora de ODBC*, ou *literal de carimbo de hora de ODBC*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo SQL|Valor de dados é uma opção válida *o valor de intervalo*; não ocorrerá o truncamento<br /><br /> Valor de dados é uma opção válida *o valor de intervalo*; o valor em um dos campos é truncado<br /><br /> O valor de dados não é um literal de intervalo válido|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] a parte de hora do carimbo de hora é truncada.  
  
 [b] a parte de data do carimbo de hora será ignorada.  
  
 [c] a parte do tempo do que o carimbo de hora é definida como zero.  
  
 [d] a parte de data do carimbo de hora é definida como a data atual.  
  
 [e] a fonte de dados/driver efetivamente aguarda até que a cadeia de caracteres inteira foi recebida (mesmo se os dados de caractere são enviados em partes por chamadas para **SQLPutData**) antes de tentar executar a conversão.  
  
 Quando os dados de caractere C são convertido em numérico, data, hora ou carimbo de hora de dados do SQL, à esquerda e à direita de espaços em branco são ignorados.  
  
 Quando os dados de caractere C são convertidos em dados binários do SQL, a cada dois bytes de dados de caracteres são convertidos em um único byte (8 bits) de dados binários. Cada dois bytes de dados de caracteres representa um número em formato hexadecimal. Por exemplo, "01" será convertido em um binário 00000001 e "FF" será convertido em um binário 11111111.  
  
 O driver sempre converte os pares de dígitos hexadecimais em bytes individuais e ignora o byte nulo de terminação. Por isso, se o comprimento da cadeia de caracteres for ímpar, o último byte da cadeia de caracteres (excluindo o byte de terminação null, se houver) não é convertido.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desaconselhável de associação de dados de caractere C para um tipo de dados binário do SQL. Normalmente, essa conversão é ineficiente e lento.
