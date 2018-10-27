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
ms.openlocfilehash: 4f1ab3b825ad85d490493c1ffa05d7e066ec0cce
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144751"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Nível de compatibilidade 1200 e superior de programação do modelo tabular
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Começando com o nível de compatibilidade 1200, metadados de tabela é usado para descrever construções de modelo, substituindo históricos metadados multidimensionais como descritores de objetos de modelo de tabela. Metadados para tabelas, colunas e relações são tabela, coluna e relação, em vez dos equivalentes Multidimensional (dimensão e atributo).  
  
Você pode criar novos modelos de nível de compatibilidade 1200 ou superior, usando as APIs de AnalysisServices, a versão mais recente dos dados de ferramentas do SSDT (SQL Server), ou alterando a **CompatibilityLevel** de uma tabela existente modelo para atualizá-lo (também é feito no SSDT). Isso associa o modelo para versões mais recentes do servidor, ferramentas e interfaces de programação.   
  
Atualizar uma solução Tabular existente é recomendado, mas não obrigatório. Soluções personalizadas que acessar ou gerenciam modelos tabulares ou bancos de dados e script existente podem ser usadas como-está. Níveis de compatibilidade anteriores são totalmente compatíveis no SQL Server 2016 usando os recursos disponíveis nesse nível. O Azure Analysis Services dá suporte apenas a nível de compatibilidade 1200 e superior.
  
 Novos modelos de tabela exige um código diferente e script, resumidas abaixo.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definições de modelo de objeto como construções de metadados de tabela  
 O modelo de objeto Tabular para modelos 1200 ou superior é exposto em JSON por meio de [Tabular Model Scripting Language](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) e, por meio da linguagem de definição de dados AMO por meio de um novo namespace, [ AnalysisServices](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Script para bancos de dados e modelos de tabela  
 TMSL é uma linguagem de script de JSON para modelos de tabela, com suporte para a criação, leitura, atualização, um operações de exclusão. Você pode atualizar os dados por meio de TMSL e invocar operações de banco de dados para anexar, desanexar, backup, restauração e sincronizar.  
  
 AMO PowerShell aceita um script TMSL como entrada.  
  
 Ver [Tabular Model Scripting Language &#40;TMSL&#41; referência](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) e [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) para obter mais informações.  
  
## <a name="query-languages"></a>Linguagens de consulta  
 DAX e MDX têm suporte para todos os modelos de tabela.  
  
## <a name="expression-language"></a>Linguagem de expressão  
 Filtros e as expressões usadas para criar objetos calculados, incluindo medidas e KPIs, são formuladas em DAX. Ver [Noções básicas sobre DAX em modelos tabulares](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) e [Data Analysis Expressions &#40;DAX&#41; no Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Código gerenciado para bancos de dados e modelos de tabela  
 O AMO inclui um novo namespace, AnalysisServices, para trabalhar com modelos de forma programática. Ver [Microsoft. AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) para obter mais informações.  
  
> [!NOTE]  
>  Bibliotecas de cliente de gerenciamento de objetos AMO (Analysis Services), o ADOMD.NET e o objeto de modelo de TOM (Tabular) agora voltados para o tempo de execução do .NET 4.0.   
  
## <a name="see-also"></a>Consulte também  
 [Documentação do desenvolvedor do Analysis Services](../../analysis-services/analysis-services-developer-documentation.md)   
 [Programação do modelo de tabela para compatibilidade níveis 1050 até 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Referência técnica ](../../analysis-services/powershell/technical-reference-ssas.md) [atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Níveis de compatibilidade dos bancos de dados e modelos de tabela](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
