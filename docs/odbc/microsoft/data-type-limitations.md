---
title: "Limitações do tipo de dados | Microsoft Docs"
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
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 558789a4f435e9fc54176b1423d71369f6b4cc22
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-limitations"></a>Limitações do tipo de dados
Os Drivers de banco de dados de área de trabalho do Microsoft ODBC impõe as seguintes limitações nos tipos de dados:  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|Todos os tipos de dados|Falhas de conversão de tipo podem resultar na coluna afetada sendo definida como NULL.|  
|BINARY|Na verdade, criar uma coluna BINARY de comprimento zero retorna uma coluna BINÁRIA de 255 bytes.|  
|DATE|O tipo de dados de data não pode ser convertido para outro tipo de dados (ou próprio), a função CONVERT.|  
|DECIMAL (numérico exato)|Sem suporte.|  
|Tipos de dados de ponto flutuante|O número de casas decimais em um número de ponto flutuante pode ser limitado por do formato numérico definido na seção internacional do painel de controle do Windows.|  
|NUMERIC|Dá suporte a precisão máxima e uma escala de 28.|  
|timestamp|O tipo de dados de carimbo de hora não pode ser convertido para si mesmo, a função CONVERT.|  
|TINYINT|Valores TINYINT são sempre não assinados.|  
|Cadeias de caracteres de comprimento zero|Quando é usado um dBASE, Microsoft Excel, Paradox ou Textdriver, inserindo uma cadeia de caracteres de comprimento zero em uma coluna, na verdade, insere um valor nulo em vez disso.|

