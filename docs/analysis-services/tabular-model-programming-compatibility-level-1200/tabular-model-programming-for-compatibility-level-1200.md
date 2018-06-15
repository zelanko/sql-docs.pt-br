---
title: Programação de modelo de tabela para o nível de compatibilidade 1200 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e0bfc84806e44ef05312da9d15d1afaa7dd9754
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039140"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Tabela de modelo de programação para 1200 de nível de compatibilidade e superior
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Começando com o nível de compatibilidade 1200, metadados de tabela é usado para descrever as construções de modelo, substituindo históricos metadados multidimensionais como descritores de objetos de modelo de tabela. Metadados de tabelas, colunas e relações são tabela, coluna e relação, em vez dos equivalentes Multidimensional (dimensão e atributo).  
  
Você pode criar novos modelos no nível de compatibilidade 1200 ou superior usando as APIs de AnalysisServices, a versão mais recente de SQL Server Data Tools (SSDT), ou alterando o **CompatibilityLevel** de uma tabela existente modelo para atualizá-lo (feita também no SSDT). Isso associa o modelo para versões mais recentes do servidor, ferramentas e interfaces de programação.   
  
Atualizar uma solução de tabela existente é recomendado, mas não é necessário. Soluções personalizadas que acessar ou gerenciar modelos tabulares ou bancos de dados e script existente podem ser usadas como-é. Níveis de compatibilidade anteriores são totalmente suportados no SQL Server 2016 usando os recursos disponíveis nesse nível. Serviços de análise do Azure oferece suporte apenas o nível de compatibilidade 1200 e superior.
  
 Novos modelos de tabela exigirá diferentes de código e script, resumido abaixo.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definições de modelo de objeto como construções de metadados de tabela  
 O modelo de objeto de tabela para modelos 1200 ou superior é exposto em JSON por meio de [linguagem de script de modelo de tabela](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e por meio da linguagem de definição de dados de AMO por meio de um novo namespace, [ AnalysisServices](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Script para modelos de tabela e bancos de dados  
 O TMSL é uma linguagem de script de JSON para modelos de tabela, com suporte para criar, ler, atualizar, de operações de exclusão. Você pode atualizar os dados por meio de TMSL e invocar operações de banco de dados para anexar, desanexar, backup, restauração e sincronizar.  
  
 PowerShell do AMO aceita script TMSL como entrada.  
  
 Consulte [linguagem de script de modelo de tabela &#40;TMSL&#41; referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) para obter mais informações.  
  
## <a name="query-languages"></a>Linguagens de consulta  
 DAX e MDX têm suporte para todos os modelos de tabela.  
  
## <a name="expression-language"></a>Linguagem de expressão  
 Filtros e as expressões usadas para criar objetos calculados, incluindo medidas e KPIs são formuladas no DAX. Consulte [compreensão do DAX em modelos de tabela](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) e [Data Analysis Expressions &#40;DAX&#41; no Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Código gerenciado para bancos de dados e modelos de tabela  
 AMO inclui um novo namespace, AnalysisServices, para trabalhar com modelos programaticamente. Consulte [Namespace Microsoft. AnalysisServices](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) para obter mais informações.  
  
> [!NOTE]  
>  Bibliotecas de cliente do Analysis Services Management Objects (AMO), o ADOMD.NET e o modelo de objeto de tabela (TOM) agora voltados para o tempo de execução do .NET 4.0.   
  
## <a name="see-also"></a>Consulte também  
 [Documentação do desenvolvedor do Analysis Services](../../analysis-services/analysis-services-developer-documentation.md)   
 [Programação de modelo de tabela para compatibilidade 1050 1103 por meio de níveis](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Referência técnica ](../../analysis-services/powershell/technical-reference-ssas.md) [atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Níveis de compatibilidade de bancos de dados e modelos de tabela](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
