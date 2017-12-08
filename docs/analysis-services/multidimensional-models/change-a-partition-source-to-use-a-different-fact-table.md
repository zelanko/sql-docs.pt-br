---
title: "Alterar uma origem de partição para usar uma tabela de fatos diferentes | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 068c4899199881270a153e866b719c15a8296f7f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>Alterar uma origem de partição para usar uma tabela de fatos diferente
  Ao criar uma partição para um cubo, você pode optar por usar uma tabela de fatos diferente. Tabelas diferentes podem ser derivadas de uma única exibição da fonte de dados, de exibições diferentes da fonte de dados ou de fontes de dados diferentes. Uma exibição da fonte de dados também pode conter tabelas diferentes de mais de uma fonte de dados.  
  
 Todas as tabelas de fatos e dimensões das partições de um cubo devem ter a mesma estrutura da tabela de fatos e das dimensões do cubo. Por exemplo, tabelas de fatos diferentes podem ter a mesma estrutura, mas conter dados de diferentes anos ou linhas de produtos.  
  
 Especifique uma tabela de fatos na página **Especificar Informações sobre a Origem** do Assistente para Partições. Nessa página, no grupo Origem da Partição próximo a **Examinar**, especifique uma fonte de dados ou a exibição da fonte de dados que deve ser examinada. Em seguida, clique em **Localizar Tabelas**e, em **Tabelas Disponíveis**, selecione a tabela que deseja usar.  
  
 Ao usar tabelas de fatos diferentes, verifique se nenhum dado está duplicado entre as partições. Por exemplo, se uma tabela de fatos contém apenas as transações de 2012 e outra tabela de fatos contém apenas as transações de 2013, essas tabelas contêm dados independentes. Do mesmo modo, tabelas de fatos para linhas de produtos ou áreas geográficas diferentes são independentes.  
  
 É possível, mas não recomendado, usar tabelas de fatos diferentes que contêm dados duplicados. Nesse caso, é necessário usar filtros nas partições para assegurar que os dados usados por uma partição não sejam usados por nenhuma outra. Para obter mais informações, consulte [Criar e gerenciar uma partição local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar uma partição local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  
