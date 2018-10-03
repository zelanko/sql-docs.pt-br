---
title: Tipos de dados Paradox | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2f3b1e63578af7c0b42f00113fbb9e87cb8003
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628504"
---
# <a name="paradox-data-types"></a>Tipos de dados Paradox
O driver do Paradox ODBC mapeia tipos de dados do Paradox para tipos de dados SQL ODBC. A tabela a seguir lista todos os tipos de dados Paradox e mostra o SQL ODBC são mapeados para os tipos de dados.  
  
|Tipo de dados Paradox|Tipo de dados ODBC|  
|-----------------------|--------------------|  
|ALFANUMÉRICO|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|BYTES [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEM DE [2]|SQL_LONGVARBINARY|  
|LÓGICO [1]|SQL_BIT|  
|LONGA [1]|SQL_INTEGER|  
|MEMORANDO [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|CURTO|SQL_SMALLINT|  
|TEMPO [1]|SQL_TIMESTAMP|  
|CARIMBO DE HORA [1]|SQL_TIMESTAMP|  
  
 [1] válido somente para versões do Paradox 5. *x*.  
  
 Válido somente para versões do Paradox 4 a [2]. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D dos *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações nos tipos de dados Paradox.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|ALFANUMÉRICO|Criando uma coluna de ALFANUMÉRICO de zero ou comprimento não especificado, na verdade, retorna uma coluna de 255 bytes.|  
|BYTES|Se você inserir NULL em uma coluna binária com o driver Paradox5, ele é alterado para 0.|  
|LONG|O valor negativo máximo com suporte pelo driver do Paradox para o tipo de dados Long no Paradox 5. *x* não é -2 ^ 31 (-2147483648), como deveria ser desde muito mapeia para os dados ODBC digite SQL_INTEGER. O valor negativo máximo com suporte por muito tempo é realmente -2 ^ 31 + 1 (-2147483647).|  
|timestamp|Quando um valor é inserido em uma coluna de carimbo de hora, o driver do Paradox, então, subsequentemente recuperado da coluna, o valor recuperado pode diferir do que o valor inserido pelo máximo de 1 segundo por causa de arredondamento.|  
  
 Mais limitações nos tipos de dados podem ser encontradas na [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
