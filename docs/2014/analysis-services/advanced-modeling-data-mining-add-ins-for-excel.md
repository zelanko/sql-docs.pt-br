---
title: Avançadas de modelagem (mineração de dados suplementos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bad97bf517bee9f8c2545d5a48acc02830dc5f58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134096"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>Modelagem avançada (Suplementos de Mineração de Dados para Excel)
  Você pode usar o **avançado** opções para criar modelos e estruturas de mineração de dados personalizados com parâmetros diferentes daqueles criados pelos assistentes de modelagem de dados. Os dois assistentes descritos nesta seção o ajudam a criar uma estrutura de mineração de dados completamente nova e um novo modelo de mineração para aplicar a uma estrutura de mineração de dados existente.  
  
## <a name="create-mining-structure"></a>Criar a Estrutura de Mineração  
 ![O botão Criar estrutura de mineração, faixa de opções mineração de dados](media/dmc-createstruct.gif "botão Criar estrutura de mineração, faixa de opções mineração de dados")  
  
 O **Assistente para criar estrutura de mineração** ajuda você a criar uma nova estrutura de mineração de dados. Uma estrutura é uma coleção dos dados extraídos de uma fonte de dados especificada.  Uma estrutura de mineração pode ser atualizada com novos dados na origem, mas quando você cria a estrutura de mineração, define tipos de dados e nomes que definem como os dados são usados para análise.  
  
 Você pode usar as seguintes fontes de dados para criar sua estrutura: uma tabela do Excel, um intervalo do Excel ou qualquer dado em uma fonte de dados externa que já foi definida como uma exibição da fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para cada estrutura, você tem a opção de separar alguns dos dados para utilizar para teste e validação. Ao criar este *conjunto de dados de controle* quando você configura suas fontes de dados, você pode garantir que todos os modelos que são baseados na estrutura sejam capazes de usar um conjunto de dados consistente para teste.  
  
 Após ter criado uma estrutura de mineração, é possível adicionar vários modelos para aplicar a diferentes métodos de análise.  
  
 Para obter mais informações sobre como usar o **criar Assistente de estrutura de mineração**, consulte [Create Mining Structure &#40;SQL Server Data Mining Add-ins&#41;](create-mining-structure-sql-server-data-mining-add-ins.md).  
  
## <a name="add-model-to-structure"></a>Adicionar modelo à estrutura  
 ![Adicionar modelo de botão de estrutura](media/dmc-addmodel.gif "Add Model ao botão de estrutura")  
  
 Quando você adiciona um novo modelo a uma estrutura, analisa os dados usando um algoritmo diferente ou com parâmetros diferentes. Essa opção é particularmente útil se você quiser criar um modelo usando um dos algoritmos não expostos nas ferramentas de cliente de mineração de dados.  
  
 Por exemplo, você pode usar qualquer um dos algoritmos suportados pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], por exemplo:  
  
-   Regressão linear  
  
-   Clustering de sequências  
  
-   Análise de associação em conjuntos de dados aninhados  
  
 Para ver quais são os tipos de estruturas de mineração disponível, você pode procurar os modelos e estruturas armazenados em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] clicando **gerenciar modelos** ou **procurar**.  
  
 Você está limitado às estruturas de mineração de dados criados durante a sessão atual ou as estruturas de mineração que foram salvas em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações, consulte [Adicionar modelo à estrutura &#40;Data Mining Add-ins para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar modelos de &#40;suplementos de mineração de dados do SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
