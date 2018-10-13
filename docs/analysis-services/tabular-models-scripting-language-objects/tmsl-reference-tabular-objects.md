---
title: Definições de objeto em tabela (TMSL) de linguagem de script de modelo | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de968c32f8c00132157a5b1b7a6682adc7148446
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851741"
---
# <a name="tmsl-reference---tabular-objects"></a>Referência TMSL – Objetos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Aplicativos que criar, consumir ou administrar bancos de dados tabulares ou que se conectam a uma instância do SQL Server 2016 Analysis Services no modo de tabela, pode usar o modelo de script TMSL (linguagem tabela) para comandos e representações de objeto no formato JSON.  
  
 Este artigo documenta os objetos principais do esquema TMSL usados nos scripts gerados pelo SQL Server Management Studio, o SQL Server Data Tools (SSDT) e o PowerShell do AMO.  
  
 As definições de objeto estão em JSON e usada nos comandos TMSL, como Create, Alter e excluam. Ver [comandos na linguagem de script de modelo de tabela &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obter uma lista de comandos.  
  
## <a name="main-objects"></a>Objetos principais  
 A tabela a seguir é uma lista dos objetos mais comumente usados no script TMSL.  
  
|||  
|-|-|  
|[O objeto de banco de dados &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Define um banco de dados Tabular no nível de compatibilidade 1200 ou superior, com base em um modelo do mesmo nível.|  
|[Objeto de modelo &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Define um modelo Tabular no nível de compatibilidade 1200 ou superior.|  
|[Fontes de dados objeto &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Define uma conexão a uma fonte de dados usada durante a importação para carregar o modelo, ou para consultas de passagem quando o modelo está no modo DirectQuery.|  
|[Objeto de tabelas &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Especifica as tabelas do modelo.|  
|[Objeto Partitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Define o armazenamento de conjuntos de linhas de tabela, incluindo tabelas calculadas.|  
|[Objeto Relationships &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Define as relações entre tabelas.|  
|[Objeto de funções &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Define as permissões, associação e os filtros de segurança que controlam o acesso a dados e operações.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
