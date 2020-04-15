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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280666"
---
# <a name="data-type-limitations"></a>Limitações de tipo de dados
Os drivers de banco de dados de desktop do Microsoft ODBC impõem as seguintes limitações aos tipos de dados:  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|Todos os tipos de dados|Falhas de conversão de tipo podem resultar na configuração da coluna afetada como NULL.|  
|BINARY|A criação de uma coluna BINÁRIA de comprimento zero retorna uma coluna BINÁRIA de 255 bytes.|  
|DATE|O tipo de dados DATE não pode ser convertido para outro tipo de dados (ou em si) pela função CONVERT.|  
|DECIMAL (Numérico Exato)|Sem suporte.|  
|Tipos de dados de pontos flutuantes|O número de casas decimais em um número de ponto flutuante pode ser limitado pelo formato de número definido na seção Internacional do Painel de Controle do Windows.|  
|NUMERIC|Suporta máxima precisão e uma escala de 28.|  
|timestamp|O tipo de dados TIMESTAMP não pode ser convertido para si mesmo pela função CONVERT.|  
|TINYINT|Os valores TINYINT são sempre não assinados.|  
|Cordas de comprimento zero|Quando um dBASE, Microsoft Excel, Paradox ou Textdriver é usado, inserir uma string de comprimento zero em uma coluna realmente insere um NULL.|
