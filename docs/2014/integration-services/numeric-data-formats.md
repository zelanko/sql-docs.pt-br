---
title: Formatos de dados numéricos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0096f34a5815237ed3865e298ecc628083ce408
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424503"
---
# <a name="numeric-data-formats"></a>Formatos de dados numéricos
  A análise rápida fornece uma análise de dados rápida e simples a um conjunto de rotinas sem diferenciação de localidade. A análise rápida suporta apenas um conjunto limitado de formatos para tipos de dados de números inteiros.  
  
## <a name="integer-data-types"></a>Tipos de Dados de Números Inteiros  
 Os tipos de dados de números inteiros que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece são DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 e DT_UI8. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
 A análise rápida suporta os seguintes formatos para tipos de dados de números inteiros:  
  
-   Zero com espaços à esquerda e à direita ou paradas de tabulação. Por exemplo, o valor "  123  " é válido. Um valor com espaços é avaliado como zero.  
  
-   Um sinal de mais, menos ou nenhum sinal. Por exemplo, os valores +123, -123 e 123 são válidos.  
  
-   Um ou mais números hindu-árabes (0-9). Por exemplo, o valor 345 é válido. Outros dados numéricos do idioma não são suportados.  
  
 Entre os formatos de dados que não são suportados estão:  
  
-   Caracteres especiais. Por exemplo, o símbolo de cifrão ($) não é suportado e o valor $20 não pode ser analisado.  
  
-   Caracteres com espaço em branco como quebra de linha, retornos de carro e espaços que não indicam uma quebra. Por exemplo, o valor " 123" não pode ser analisado.  
  
-   Representações hexadecimais de números inteiros. Por exemplo, o valor 2EE não pode ser analisado.  
  
-   Representação de notação científica de números inteiros. Por exemplo, o valor 1E+10 não pode ser analisado.  
  
 Os seguintes formatos são formatos de dados de saída para números inteiros:  
  
-   Um sinal de menos para números negativos e nenhum sinal para números positivos.  
  
-   Nenhum espaço em branco.  
  
-   Um ou mais números hindu-árabes (0-9).  
  
  
