---
title: "Definir atribuições e outros comandos de Script | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1084744ca372d6ac89d2f7a2d625c01383d2079c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="define-assignments-and-other-script-commands"></a>Definir atribuições e outros comandos de script
  Para criar um script vazio, no Designer de Cubo, na guia **Cálculos** , clique no ícone **Novo ScriptCommand** na barra de ferramentas. Quando você criar um novo script, inicialmente, ele será exibido com um título em branco no painel **Organizador de Script** da guia Cálculos. Os caracteres que você digitar no painel Expressões de Cálculo serão visíveis como o nome do item no **Organizador de Script**. Portanto, convém digitar um nome comentado na primeira linha para facilitar a identificação do script no painel **Organizador de Script** . Para obter mais informações, consulte [Introdução ao script MDX no Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Para obter mais informações sobre questões de desempenho relacionadas a cálculos e consultas MDX, consulte a seção “Writing Efficient MDX” (Escrevendo um MDX eficiente) no [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(Guia de desempenho do SQL Server 2005 Analysis Services).  
  
> [!IMPORTANT]  
>  Quando você inicialmente muda para a guia **Cálculos** do Designer de Cubo, o painel **Organizador de Script** contém um único script com um comando CALCULATE. O comando CALCULATE controla a agregação das células do cubo e deve ser editado somente se você pretender especificar manualmente como o cubo será agregado.  
  
 Você pode usar o painel Expressões de Cálculo para construir uma expressão em sintaxe MDX. Ao criar a expressão, você pode copiar ou arrastar os componentes, funções e modelos do cubo do painel **Ferramentas de Cálculo** para o painel Expressões de Cálculo. Isso adicionará o script do item ao painel Expressões de Cálculo no local para onde você o arrastar ou copiar. Substitua os argumentos e seus delimitadores (« e ») pelos valores apropriados.  
  
> [!IMPORTANT]  
>  Ao gravar uma expressão que contém várias instruções usando o painel Expressões de Cálculo, certifique-se de que todas as linhas do script MDX, exceto a última, terminam com um ponto-e-vírgula (;). Os cálculos são concatenados em um único script MDX e cada script possui um ponto-e-vírgula anexado a ele para garantir a compilação correta do script MDX. Se você adicionar um ponto-e-vírgula à última linha do script no painel Expressões de Cálculo, o cubo será construído e implantado corretamente, mas não será possível executar consultas nele.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
