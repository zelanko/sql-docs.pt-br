---
title: Tipos de dados do Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290926"
---
# <a name="paradox-data-types"></a>Tipos de dados Paradox
O driver ODBC Paradox mapeia tipos de dados do Paradox para tipos de dados SQL ODBC. A tabela a seguir lista todos os tipos de dados do Paradox e mostra os tipos de dados ODBC do SQL aos quais eles estão mapeados.  
  
|Tipo de dados do Paradox|Tipo de dados ODBC|  
|-----------------------|--------------------|  
|ALFANUMÉRICO|SQL_VARCHAR|  
|INCREMENTO AUTOMÁTICO [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|BYTES [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEM [2]|SQL_LONGVARBINARY|  
|LÓGICO [1]|SQL_BIT|  
|LONGO [1]|SQL_INTEGER|  
|MEMORANDO [2]|SQL_LONGVARCHAR|  
|DINHEIRO [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|BAIXO|SQL_SMALLINT|  
|HORA [1]|SQL_TIMESTAMP|  
|CARIMBO DE DATA/HORA [1]|SQL_TIMESTAMP|  
  
 [1] válido somente para versões 5 do Paradox. *x*.  
  
 [2] válido somente para versões 4 do Paradox. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados SQL ODBC. Todas as conversões no Apêndice D da *referência do programador de ODBC* têm suporte para os tipos de dados ODBC SQL listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações dos tipos de dados do Paradox.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|ALFANUMÉRICO|A criação de uma coluna alfanumérica de comprimento zero ou não especificado realmente retorna uma coluna de 255 bytes.|  
|BYTES|Se você inserir NULL em uma coluna binária com o driver Paradox5, ele será alterado para 0.|  
|LONG|O valor negativo máximo com suporte do driver do Paradox para o tipo de dados Long no Paradox 5. *x* não é-2 ^ 31 (-2147483648), pois deve ser desde que haja mapas longos para o tipo de dados ODBC SQL_INTEGER. O valor máximo negativo com suporte para Long é, na verdade,-2 ^ 31 + 1 (-2147483647).|  
|timestamp|Quando um valor é inserido em uma coluna de carimbo de data/hora pelo driver do Paradox e, posteriormente, recuperado da coluna, o valor recuperado pode ser diferente do valor inserido pelo máximo de 1 segundo devido ao arredondamento.|  
  
 Mais limitações sobre tipos de dados podem ser encontradas em [limitações de tipo de dados](../../odbc/microsoft/data-type-limitations.md).
