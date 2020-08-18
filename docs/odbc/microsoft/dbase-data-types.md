---
description: Tipos de dados do dBASE
title: Tipos de dados do dBASE | Microsoft Docs
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
ms.openlocfilehash: 9eca7d603a136bd1921ee93656d38f59efcda5f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412762"
---
# <a name="dbase-data-types"></a>Tipos de dados do dBASE
A tabela a seguir mostra como os tipos de dados do dBASE são mapeados para tipos de dados ODBC do SQL. Observe que nem todos os tipos de dados SQL ODBC têm suporte.  
  
|tipo de dados do dBASE|Tipo de dados ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|LÓGICO|SQL_BIT|  
|CAMPOS|SQL_LONGVARCHAR|  
|NUMERIC (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] válido somente para o dBASE versão 5. *x*  
  
 A precisão no dBASE III permite números com expoentes de até dois dígitos e em números do dBASE IV com expoentes de até três dígitos. Como os números são armazenados como texto, eles são convertidos em números. Se o número a ser convertido não couber em um campo, poderão ocorrer resultados não explicados.  
  
 Embora o dBASE permita que uma precisão e uma escala sejam especificadas com um tipo de dados numérico, não há suporte para ele no driver do dBASE do ODBC. O driver ODBC dBASE sempre retorna uma precisão de 15 e uma escala de 0 para um tipo de dados numérico.  
  
 Uma coluna criada com o tipo de dados numeric usando o driver ODBC dBASE é mapeada para o tipo de dados SQL_DOUBLE ODBC. Portanto, os dados nesta coluna estão sujeitos ao arredondamento. Esse comportamento não é o mesmo que o tipo de dados NUMERIC no dBASE (tipo N), que é um formato binário codificado (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados SQL ODBC. Todas as conversões no Apêndice D da *referência do programador de ODBC* têm suporte para os tipos de dados ODBC SQL listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações em tipos de dados do dBASE.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|CHAR|Na verdade, a criação de uma coluna CHAR com comprimento zero ou não especificado retorna uma coluna de 254 bytes.|  
|Dados criptografados|O driver do dBASE não oferece suporte a tabelas criptografadas do dBASE.|  
|LÓGICO|O driver do dBASE não pode criar um índice em uma coluna lógica.|  
|CAMPOS|O comprimento máximo de uma coluna de memorando é de 65.500 bytes.|  
  
 Mais limitações sobre tipos de dados podem ser encontradas em [limitações de tipo de dados](../../odbc/microsoft/data-type-limitations.md).
