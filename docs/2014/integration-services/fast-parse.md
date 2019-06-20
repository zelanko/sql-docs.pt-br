---
title: Análise rápida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b13ddc498962ca23e6bc1f5e7a10d88af47ff7d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058865"
---
# <a name="fast-parse"></a>Fast Parse
  A análise rápida fornece um conjunto de rotinas simples e rápidas para analisar dados. Essas rotinas não são sensíveis à localidade e aceitam apenas um subconjunto de formatos de data, hora e inteiro.  
  
## <a name="requirements-and-limitations"></a>Requisitos e limitações  
 Ao se implementar a análise rápida, o pacote perde sua habilidade para interpretar data, hora e dados numéricos em formatos específicos à localidade e em formatos ISO 8601 básicos e estendidos, mas o pacote melhora seu desempenho. Por exemplo, a análise rápida oferece suporte somente aos formatos mais comuns utilizados para representar data como YYYYMMDD e YYYY-MM-DD, não executa análise específica do local, não reconhece caracteres especiais em dados de moeda e não pode converter representação hexadecimal ou científica de inteiros.  
  
 A análise rápida só está disponível quando você usa o fonte Arquivo Simples ou a transformação de Conversão de Dados. O aumento no desempenho pode ser significativo e você pode considerar o uso da análise rápida nesses componentes de fluxo de dados se desejar.  
  
 Se o fluxo de dados no pacote requer análise sensível a localidade, a análise padrão é recomendada em lugar da análise rápida. Por exemplo, a análise rápida não reconhece dados sensíveis ao local, que incluem símbolos decimais como a vírgula, formatos de data que não sejam ano-mês-dia e símbolos de moeda.  
  
 Representações truncadas que implicam em uma ou mais partes da data, como um século, um ano ou um mês, não são reconhecidas pela análise rápida. Por exemplo, a análise rápida não reconhece o formato ' **-YYMM**', que especifica um ano e um mês em um século implícito, nem ' **--MM**', que especifica um mês em um ano implícito. Porém, algumas representações com precisão reduzida são reconhecidas. Por exemplo, a análise rápida reconhece o formato 'hhmm;', que indica somente hora e minuto e '**YYYY**', que indica somente o ano.  
  
 A análise rápida é especificada ao nível de coluna. Na fonte Flat File e na transformação de Conversão de Dados, você pode especificar a Análise rápida nas colunas de saída. Entradas e saídas podem incluir colunas sensíveis a local e colunas não sensíveis a local.  
  
 Para obter mais informações sobre os formatos de dados suportados pela Análise Rápida, veja [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) e [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir a análise rápida](../../2014/integration-services/set-fast-parse.md)  
  
  
