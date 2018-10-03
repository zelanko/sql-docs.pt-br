---
title: Tipos de dados de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: e6c2a73aec119b7572cad93dedb2994235329cb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826024"
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
