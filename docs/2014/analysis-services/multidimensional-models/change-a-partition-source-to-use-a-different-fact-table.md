---
title: Alterar uma origem de partição para usar uma tabela de fatos diferentes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7355f5f7430a5e74cd06ffa73c1b6ed68e11a7c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122739"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>Alterar uma origem de partição para usar uma tabela de fatos diferente
  Ao criar uma partição para um cubo, você pode optar por usar uma tabela de fatos diferente. Tabelas diferentes podem ser derivadas de uma única exibição da fonte de dados, de exibições diferentes da fonte de dados ou de fontes de dados diferentes. Uma exibição da fonte de dados também pode conter tabelas diferentes de mais de uma fonte de dados.  
  
 Todas as tabelas de fatos e dimensões das partições de um cubo devem ter a mesma estrutura da tabela de fatos e das dimensões do cubo. Por exemplo, tabelas de fatos diferentes podem ter a mesma estrutura, mas conter dados de diferentes anos ou linhas de produtos.  
  
 Especifique uma tabela de fatos na página **Especificar Informações sobre a Origem** do Assistente para Partições. Nessa página, no grupo Origem da Partição próximo a **Examinar**, especifique uma fonte de dados ou a exibição da fonte de dados que deve ser examinada. Em seguida, clique em **Localizar Tabelas**e, em **Tabelas Disponíveis**, selecione a tabela que deseja usar.  
  
 Ao usar tabelas de fatos diferentes, verifique se nenhum dado está duplicado entre as partições. Por exemplo, se uma tabela de fatos contém apenas as transações de 2012 e outra tabela de fatos contém apenas as transações de 2013, essas tabelas contêm dados independentes. Do mesmo modo, tabelas de fatos para linhas de produtos ou áreas geográficas diferentes são independentes.  
  
 É possível, mas não recomendado, usar tabelas de fatos diferentes que contêm dados duplicados. Nesse caso, é necessário usar filtros nas partições para assegurar que os dados usados por uma partição não sejam usados por nenhuma outra. Para obter mais informações, consulte [Create and Manage a Local Partition &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar uma partição Local &#40;do Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  