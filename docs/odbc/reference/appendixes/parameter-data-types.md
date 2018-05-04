---
title: Tipos de dados de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a43fdab2fd7ffeaf409bde41c06386fad23d3c3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-data-types"></a>Tipos de dados de parâmetro
Embora cada parâmetro é especificado com **SQLBindParameter** é definido usando um tipo de dados do SQL, os parâmetros em uma instrução SQL ter nenhum intrínsecos tipo de dados. Portanto, os marcadores de parâmetro podem ser incluídos em uma instrução SQL somente se seus tipos de dados podem ser inferidos de outro operando na instrução. Por exemplo, em uma expressão aritmética, como? + COLUMN1, o tipo de dados do parâmetro pode ser deduzido do tipo de dados da coluna nomeada representado por COLUMN1. Um aplicativo não pode usar um marcador de parâmetro se o tipo de dados não pode ser determinado.  
  
 A tabela a seguir descreve como um tipo de dados é determinado para vários tipos de parâmetros, de acordo com o SQL-92. Para uma especificação de mais abrangente sobre inferir o tipo de parâmetro quando outras cláusulas SQL são usadas, consulte a especificação de SQL-92.  
  
|Local do parâmetro|Presume-se que o tipo de dados|  
|---------------------------|-----------------------|  
|Um operando de um operador de comparação ou aritmética binário|Mesmo que o outro operando|  
|O primeiro operando em uma **entre** cláusula|Mesmo que o segundo operando|  
|O operando de segundo ou de terceiro em um **entre** cláusula|Mesmo que o primeiro operando|  
|Uma expressão usada com **IN**|Mesmo que o primeiro valor ou a coluna de resultados da subconsulta|  
|Um valor usado com **IN**|Mesmo que a expressão ou o primeiro valor, se houver um marcador de parâmetro na expressão|  
|Um valor padrão usado com **como**|VARCHAR|  
|Um valor de atualização usado com **atualizar**|Mesmo que a coluna de atualização|
