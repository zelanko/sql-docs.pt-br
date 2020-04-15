---
title: Tipos de dados de parâmetros | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303577"
---
# <a name="parameter-data-types"></a>Tipos de dados do parâmetro
Embora cada parâmetro especificado com **SQLBindParameter** seja definido usando um tipo de dados SQL, os parâmetros em uma declaração SQL não têm nenhum tipo de dados intrínseco. Portanto, os marcadores de parâmetros só podem ser incluídos em uma declaração SQL se seus tipos de dados puderem ser inferidos de outro operand na declaração. Por exemplo, em uma expressão aritmética como? + COLUNA1, o tipo de dados do parâmetro pode ser inferido a partir do tipo de dados da coluna nomeada representada pela COLUNA1. Um aplicativo não pode usar um marcador de parâmetro se o tipo de dados não puder ser determinado.  
  
 A tabela a seguir descreve como um tipo de dados é determinado para vários tipos de parâmetros, de acordo com o SQL-92. Para obter uma especificação mais abrangente sobre a inferência do tipo de parâmetro quando outras cláusulas SQL forem usadas, consulte a especificação SQL-92.  
  
|Localização do parâmetro|Tipo de dados presumido|  
|---------------------------|-----------------------|  
|Um operand de um operador de aritmética binária ou de comparação|O mesmo que o outro operand|  
|O primeiro operador em uma cláusula **BETWEEN**|O mesmo que o segundo operand|  
|O segundo ou terceiro operand em uma cláusula **BETWEEN**|O mesmo que o primeiro operand|  
|Uma expressão usada com **IN**|O mesmo que o primeiro valor ou a coluna de resultado da subquery|  
|Um valor usado com **IN**|O mesmo que a expressão ou o primeiro valor se houver um marcador de parâmetro na expressão|  
|Um valor padrão usado com **LIKE**|VARCHAR|  
|Um valor de atualização usado com **UPDATE**|O mesmo que a coluna de atualização|
