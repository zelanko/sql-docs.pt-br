---
title: dBASE Data Types | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307687"
---
# <a name="dbase-data-types"></a>Tipos de dados do dBASE
A tabela a seguir mostra como os tipos de dados dBASE são mapeados para os tipos de dados SQL do ODBC. Observe que nem todos os tipos de dados SQL ODBC são suportados.  
  
|tipo de dados dBASE|Tipo de dados ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT[1]|SQL_DOUBLE|  
|Lógico|SQL_BIT|  
|Memorando|SQL_LONGVARCHAR|  
|Numérico (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] Válido apenas para dBASE versão 5. *x*  
  
 A precisão no dBASE III permite números com expoentes de até dois dígitos e em números dBASE IV com expoentes de até três dígitos. Como os números são armazenados como texto, eles são convertidos em números. Se o número a converter não se encaixar em um campo, resultados inexplicáveis podem ocorrer.  
  
 Embora o dBASE permita que uma precisão e uma escala sejam especificadas com um tipo de dados NUMERIC, ele não é suportado pelo driver oDBC dBASE. O driver dBASE ODBC sempre retorna uma precisão de 15 e uma escala de 0 para um tipo de dados NUMERIC.  
  
 Uma coluna criada com o tipo de dados numérico usando o driver de driver oDBC dBASE mapeia para o SQL_DOUBLE tipo de dados ODBC. Assim, os dados desta coluna estão sujeitos a arredondamento. Esse comportamento não é o mesmo do tipo de dados NUMERIC no dBASE (tipo N), que é Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna os tipos de dados ODBC SQL. Todas as conversões no apêndice D da *Referência do Programador ODBC* são suportadas para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações nos tipos de dados dBASE.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|CHAR|A criação de uma coluna CHAR de comprimento zero ou não especificado realmente retorna uma coluna de 254 bytes.|  
|Dados criptografados|O driver dBASE não suporta tabelas dBASE criptografadas.|  
|Lógico|O driver dBASE não pode criar um índice em uma coluna LOGICAL.|  
|Memorando|O comprimento máximo de uma coluna MEMO é de 65.500 bytes.|  
  
 Mais limitações nos tipos de dados podem ser encontradas nas [Limitações do Tipo de Dados](../../odbc/microsoft/data-type-limitations.md).
