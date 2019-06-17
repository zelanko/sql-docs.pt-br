---
title: Tipos de dados de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.openlocfilehash: e1f1097927f61355cf4a50f4287397d823fd3177
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632409"
---
# <a name="parameter-data-types"></a>Tipos de dados do parâmetro
Embora cada parâmetro especificado com **SQLBindParameter** é definido usando um tipo de dados SQL, os parâmetros em uma instrução SQL ter nenhum intrínseco tipo de dados. Portanto, os marcadores de parâmetro podem ser incluídos em uma instrução SQL somente se seus tipos de dados podem ser inferidos de outro operando na instrução. Por exemplo, em uma expressão aritmética, como? + COLUMN1, o tipo de dados do parâmetro pode ser inferido do tipo de dados da coluna nomeada representado por COLUMN1. Um aplicativo não é possível usar um marcador de parâmetro se o tipo de dados não puder ser determinado.  
  
 A tabela a seguir descreve como um tipo de dados é determinado para vários tipos de parâmetros, de acordo com o SQL-92. Para uma especificação mais abrangente de inferir o tipo de parâmetro quando outras cláusulas SQL são usadas, consulte a especificação SQL-92.  
  
|Local do parâmetro|Presume-se o tipo de dados|  
|---------------------------|-----------------------|  
|Um operando de um operador de comparação ou aritmética binário|Mesmo que o outro operando|  
|O primeiro operando em uma **BETWEEN** cláusula|Mesmo que o segundo operando|  
|O segundo ou terceiro operando em uma **BETWEEN** cláusula|Mesmo que o primeiro operando|  
|Uma expressão usada com **IN**|Mesmo que o primeiro valor ou a coluna de resultados da subconsulta|  
|Um valor usado com **IN**|Mesmo que a expressão ou o primeiro valor, se houver um marcador de parâmetro na expressão|  
|Um valor padrão usado com **como**|VARCHAR|  
|Usado com um valor de atualização **atualizar**|Mesmo que a coluna de atualização|
