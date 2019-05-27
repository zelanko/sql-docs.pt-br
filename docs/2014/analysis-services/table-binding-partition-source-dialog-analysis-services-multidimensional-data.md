---
title: Tabela de detalhes (caixa de diálogo de origem de partição) de associação (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitiontableselection.f1
ms.assetid: 67d05389-81ae-4a6b-947b-986d37ec72b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f8ea36c8c3d49d4903379ed4450548fc760937a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067864"
---
# <a name="table-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Detalhes de Associação de Tabela (caixa de diálogo Origem da Partição) (Analysis Services - Dados Multidimensionais)
  Use a opção **Associação de Tabela** na caixa de diálogo **Origem da Partição** para especificar a tabela de fatos que fornece os dados para a partição. É possível exibir este painel selecionando **Associação de Tabela** da opção **Tipo de Associação** na caixa de diálogo **Origem da Partição** .  
  
## <a name="options"></a>Opções  
 **grupo de medidas**  
 Exibe o grupo de medidas desta partição.  
  
 **Look in**  
 Selecione a fonte de dados ou exibição da fonte de dados que contém as tabelas de origem desta partição. A exibição da fonte de dados usada pelo grupo de medidas selecionado é selecionada por padrão.  
  
 **Filtrar tabelas**  
 Digite a cadeia de caracteres usada para restringir, por nome de tabela, as tabelas exibidas em **Tabelas disponíveis**.  
  
 **Localizar tabelas**  
 Selecione para atualizar a lista de tabelas em **Tabelas disponíveis**, restringindo ainda mais a lista, se uma cadeia de caracteres tiver sido especificada em **Filtrar tabelas**.  
  
 **Tabelas disponíveis**  
 Clique para selecionar a tabela a ser usada como uma tabela de origem para a partição.  
  
 Se nenhum filtro for especificado em **Filtrar tabelas**, todas as tabelas da fonte de dados ou exibição da fonte de dados especificadas em **Examinar** que forem semelhantes em estrutura à tabela de fatos usada pelo grupo de medidas especificado em **Grupo de medidas** serão listadas.  
  
 Se um filtro for especificado em **Filtrar tabelas**, a lista será restringida ainda mais comparando o filtro com os nomes das tabelas que atendem aos critérios acima. Apenas as tabelas que contêm a cadeia de caracteres especificada em **Filtrar tabelas** são exibidas.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo fonte de partição &#40;Analysis Services - dados multidimensionais&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
