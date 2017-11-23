---
title: Tipos de dados Paradox | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9099d9a84fb79132249c74d1d24cc240bcf8aae0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="paradox-data-types"></a>Tipos de dados Paradox
O driver ODBC Paradox mapeia tipos de dados do Paradox para tipos de dados SQL ODBC. A tabela a seguir lista todos os tipos de dados Paradox e mostra o ODBC SQL são mapeados para os tipos de dados.  
  
|Tipo de dados Paradox|Tipo de dados ODBC|  
|-----------------------|--------------------|  
|ALFANUMÉRICO|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|BYTES [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEM DE [2]|SQL_LONGVARBINARY|  
|LÓGICA [1]|SQL_BIT|  
|LONGA [1]|SQL_INTEGER|  
|MEMORANDO [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|CURTO|SQL_SMALLINT|  
|TEMPO [1]|SQL_TIMESTAMP|  
|CARIMBO DE HORA [1]|SQL_TIMESTAMP|  
  
 Válido somente para versões Paradox 5 a [1]. *x*.  
  
 Válido somente para versões Paradox 4 a [2]. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D do *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações nos tipos de dados Paradox.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|ALFANUMÉRICO|Criando uma coluna ALFANUMÉRICA de zero ou comprimento especificado, na verdade, retorna uma coluna de 255 bytes.|  
|BYTES|Se você inserir NULL em uma coluna binária com o driver Paradox5, ele será alterado para 0.|  
|LONG|O valor negativo máximo com suporte pelo driver para o tipo de dados Long Paradox 5 Paradox. *x* não é de -2 ^ 31 (-2147483648), pois ele deve ser desde longo mapas para os dados ODBC tipo SQL_INTEGER. O valor negativo máximo com suporte por muito tempo é realmente -2 ^ 31 + 1 (-2147483647).|  
|timestamp|Quando um valor é inserido em uma coluna de carimbo de hora pelo driver Paradox e subsequentemente recuperado da coluna, o valor recuperado pode diferir do que o valor inserido por até 1 segundo em razão do arredondamento.|  
  
 Mais limitações nos tipos de dados podem ser encontradas no [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).

