---
title: Limitações do tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 309a539cc0f5758fd521e408e64f7155bc9ab9f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900621"
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
|TIMESTAMP|O tipo de dados de carimbo de hora não pode ser convertido para si mesmo, a função CONVERT.|  
|TINYINT|Valores TINYINT são sempre não assinados.|  
|Cadeias de caracteres de comprimento zero|Quando é usado um dBASE, Microsoft Excel, Paradox ou Textdriver, inserindo uma cadeia de caracteres de comprimento zero em uma coluna, na verdade, insere um valor nulo em vez disso.|
