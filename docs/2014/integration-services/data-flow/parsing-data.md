---
title: Análise de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ad7af47f1c35e0e53ffb73e751cbc754aebfe772
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914904"
---
# <a name="parsing-data"></a>Análise de dados
  Os fluxos de dados em pacotes extraem e carregam dados entre armazenamentos de dados heterogêneos, que podem usar uma variedade de tipos de dados padrão e personalizados. Em um fluxo de dados, as fontes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fazem o trabalho de extração dos dados, análise dos dados da cadeia de caracteres e conversão de dados para um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As transformações subsequentes podem analisar os dados para convertê-los em um tipo diferente de dados ou para criar cópias de coluna com tipos diferentes de dados. As expressões usadas em componentes também podem lançar argumentos e operandos para os tipos diferentes de dados. Finalmente, quando os dados são carregados no repositório de dados, o destino pode analisar os dados para convertê-los em um tipo de dados usado pelo destino. Para obter mais informações, consulte [Integration Services Data Types](integration-services-data-types.md).  
  
## <a name="types-of-parsing"></a>Tipos de análise  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece dois tipos de análises para conversão de dados: Análise rápida e Análise padrão.  
  
-   A análise rápida é um conjunto simples de rotinas de análise que não oferece suporte a conversões de tipos de dados específicas de localidade, e só oferece suporte aos formatos de data e hora usados com mais frequência. Para obter mais informações, consulte [Fast Parse](../fast-parse.md).  
  
-   A análise padrão é um conjunto rico de rotinas de análise que oferecem suporte a todas as conversões de tipos de dados fornecidas pelas APIs de conversão de tipos de dados de Automação, disponíveis no Oleaut32.dll e Ole2dsip.dll. Para obter mais informações, consulte [Standard Parse](../standard-parse.md).  
  
  
