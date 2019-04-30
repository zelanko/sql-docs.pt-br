---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc4b4c7a5c1074a62bf0e84d265840109f65ea55
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126309"
---
# <a name="dbase-data-types"></a>Tipos de dados do dBASE
A tabela a seguir mostra como os tipos de dados do dBASE são mapeados para tipos de dados SQL ODBC. Observe que nem todos os tipos de dados ODBC SQL têm suporte.  
  
|tipo de dados do dBASE|Tipo de dados ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|LÓGICA|SQL_BIT|  
|MEMORANDO|SQL_LONGVARCHAR|  
|NUMÉRICO (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] válido somente para a versão 5 do dBASE. *x*  
  
 Precisão em dBASE III permite números com backup para expoentes de dois dígitos e dBASE IV números com até expoentes de três dígitos. Como os números são armazenados como texto, eles são convertidos em números. Se o número a ser convertido não couber em um campo, podem ocorrer resultados inexplicáveis.  
  
 Embora dBASE permita uma precisão e uma escala a ser especificado com um tipo de dados numéricos, não há suporte pelo driver ODBC do dBASE. O driver do dBASE ODBC sempre retorna uma precisão de 15 e uma escala de 0 para um tipo de dados numéricos.  
  
 Uma coluna criada com o tipo de dados numéricos usando os mapas de driver do dBASE ODBC para o tipo de dados ODBC SQL_DOUBLE. Portanto, os dados nesta coluna estão sujeitas a arredondamento. Esse comportamento não é o mesmo como que os dados numéricos do tipo no dBASE (tipo N), que é o Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D dos *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações no dBASE, tipos de dados.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|CHAR|Criação de uma coluna CHAR igual a zero ou comprimento não especificado, na verdade, retorna uma coluna de bytes de 254.|  
|Dados criptografados|O driver do dBASE não oferece suporte a tabelas do dBASE criptografado.|  
|LÓGICA|O driver do dBASE não é possível criar um índice em uma coluna de lógica.|  
|MEMORANDO|O comprimento máximo de uma coluna de memorando é 65.500 bytes.|  
  
 Mais limitações nos tipos de dados podem ser encontradas na [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
