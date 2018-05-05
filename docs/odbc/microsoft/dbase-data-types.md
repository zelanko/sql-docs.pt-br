---
title: Tipos de dados do dBASE | Microsoft Docs
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
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60240eb9763d2d0b581765bde3a6d0958567f08e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dbase-data-types"></a>Tipos de dados do dBASE
A tabela a seguir mostra como os tipos de dados do dBASE são mapeados para tipos de dados SQL ODBC. Observe que nem todos os tipos de dados SQL ODBC têm suporte.  
  
|tipo de dados do dBASE|Tipo de dados ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|LÓGICA|SQL_BIT|  
|MEMORANDO|SQL_LONGVARCHAR|  
|NUMÉRICO (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] válido somente para a versão 5 do dBASE. *x*  
  
 Precisão no dBASE III permite números com backup em dois dígitos expoentes e dBASE IV números com até três dígitos expoentes. Como os números são armazenados como texto, eles são convertidos em números. Se o número a ser convertido não couber em um campo, podem ocorrer resultados inexplicáveis.  
  
 Embora dBASE permite uma precisão e uma escala a ser especificado com um tipo de dados NUMÉRICO, ele não tem suporte pelo driver ODBC dBASE. O driver ODBC para dBASE sempre retorna uma precisão de 15 e uma escala de 0 para um tipo de dados NUMÉRICO.  
  
 Uma coluna criada com o tipo de dados numéricos usando os mapas de driver ODBC dBASE para o tipo de dados ODBC SQL_DOUBLE. Assim, os dados nesta coluna estão sujeito a arredondamentos. Esse comportamento não é o mesmo como que os dados numéricos do tipo no dBASE (tipo N), que é o Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D do *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações em dBASE tipos de dados.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|CHAR|Criação de uma coluna CHAR de zero ou uma coluna de 254 bytes realmente retorna um comprimento especificado.|  
|Dados criptografados|O driver dBASE não dá suporte a tabelas dBASE criptografados.|  
|LÓGICA|O driver dBASE não é possível criar um índice em uma coluna lógica.|  
|MEMORANDO|O comprimento máximo de uma coluna de memorando é 65.500 bytes.|  
  
 Mais limitações nos tipos de dados podem ser encontradas no [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
