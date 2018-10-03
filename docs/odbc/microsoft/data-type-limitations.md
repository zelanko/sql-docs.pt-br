---
title: Limitações do tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4ce0eb96832f4a6b9c1953b0a9a9d0af65cb3b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687971"
---
# <a name="data-type-limitations"></a>Limitações de tipo de dados
Os Drivers de banco de dados de área de trabalho do Microsoft ODBC impõe as seguintes limitações nos tipos de dados:  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|Todos os tipos de dados|Falhas de conversão de tipo podem resultar na coluna afetada que está sendo definida como NULL.|  
|BINARY|Na verdade, a criação de uma coluna BINÁRIA de comprimento zero retorna uma coluna BINÁRIA de 255 bytes.|  
|DATE|O tipo de dados de data não pode ser convertido para outro tipo de dados (ou em si), a função CONVERT.|  
|DECIMAL (Numeric exato)|Sem suporte.|  
|Tipos de dados de ponto flutuante|O número de casas decimais em um número de ponto flutuante pode ser limitado pelo formato numérico definido na seção internacional do painel de controle do Windows.|  
|NUMERIC|Dá suporte a precisão máxima e uma escala de 28.|  
|timestamp|O tipo de dados de carimbo de hora não pode ser convertido para si mesmo, a função CONVERT.|  
|TINYINT|Valores TINYINT são sempre não assinados.|  
|Cadeias de caracteres de comprimento zero|Quando é usado um dBASE, Microsoft Excel, Paradox ou Textdriver, inserindo uma cadeia de caracteres de comprimento zero em uma coluna, na verdade, insere um valor nulo em vez disso.|
