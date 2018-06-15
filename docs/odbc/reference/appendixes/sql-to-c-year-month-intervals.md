---
title: 'SQL para c: ano-mês intervalos | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da1a3378ba16a360ff2e307219ea350fa6ed1efd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910011"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL para c: ano-mês intervalos
Os identificadores para os tipos de dados SQL ODBC ano-mês intervalo são:  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 A tabela a seguir mostra o ODBC C para o ano-mês o intervalo de dados do SQL pode ser convertido de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|Parte de campos à direita não truncado<br /><br /> Parte de campos à direita truncado<br /><br /> Precisão do destino principal não é grande o suficiente para armazenar dados de origem|data<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|Precisão do intervalo foi um único campo e os dados foi convertidos sem truncamento<br /><br /> Precisão do intervalo foi um único campo e inteiro truncado<br /><br /> Precisão do intervalo não era um único campo|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados em bytes<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Bytes de comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de frações) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de frações) > = *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de frações) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de frações) > = *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de ano-mês de um tipo SQL pode ser convertido em qualquer tipo de intervalo C mês do ano.  
  
 [b] se a precisão do intervalo é um único campo (um dos anos ou meses), o intervalo de tipo SQL pode ser convertido em qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  
  
 A conversão padrão de um intervalo de tipo de SQL é o tipo de dados de intervalo de C correspondente. O aplicativo, em seguida, associa a coluna ou parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado da descartar) para apontar para a estrutura SQL_INTERVAL_STRUCT inicializada (ou transmite um ponteiro para a estrutura de SQL _ INTERVAL_STRUCT como o *TargetValuePtr* argumento em uma chamada para **SQLGetData**).
