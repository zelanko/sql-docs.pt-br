---
description: Limitações de tipo de dados
title: Limitações de tipo de dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412782"
---
# <a name="data-type-limitations"></a>Limitações de tipo de dados
Os drivers de banco de dados do Microsoft ODBC Desktop impõem as seguintes limitações nos tipos de dado:  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|Todos os tipos de dados|As falhas de conversão de tipo podem resultar na definição da coluna afetada como NULL.|  
|BINARY|A criação de uma coluna binária de comprimento zero retorna, na verdade, uma coluna binária de 255 bytes.|  
|DATE|O tipo de dados DATE não pode ser convertido em outro tipo de dados (ou em si) pela função CONVERT.|  
|DECIMAL (numérico exato)|Não há suporte.|  
|Tipos de dados de ponto flutuante|O número de casas decimais em um número de ponto flutuante pode ser limitado pelo formato de número definido na seção internacional do painel de controle do Windows.|  
|NUMERIC|Dá suporte à precisão máxima e a uma escala de 28.|  
|timestamp|O tipo de dados TIMESTAMP não pode ser convertido em si mesmo pela função CONVERT.|  
|TINYINT|Os valores TINYINT sempre são não assinados.|  
|Cadeias de caracteres de comprimento zero|Quando um dBASE, o Microsoft Excel, o Paradox ou o textdriver é usado, a inserção de uma cadeia de caracteres de comprimento zero em uma coluna insere, na verdade, um NULL.|
