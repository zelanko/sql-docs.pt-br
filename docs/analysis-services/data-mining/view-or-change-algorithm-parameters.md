---
title: "Exibir ou alterar par&#226;metros do algoritmo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "algoritmos [mineração de dados]"
  - "modelos de mineração [Analysis Services], algoritmos"
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 15
---
# Exibir ou alterar par&#226;metros do algoritmo
  Você pode alterar os parâmetros fornecidos com os algoritmos usados para criar modelos de mineração de dados para personalizar os resultados do modelo.  
  
 Os parâmetros de algoritmo fornecidos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não alteram apenas as propriedades no modelo: eles podem ser usados para alterar significativamente a maneira como dados são processados, agrupados e exibidos. Por exemplo, você pode usar parâmetros de algoritmo para fazer o seguinte:  
  
-   Alterar o método de análise, como o método de clustering.  
  
-   Controlar o comportamento da seleção de recursos.  
  
-   Especificar o tamanho de conjuntos de itens ou a probabilidade de regras.  
  
-   Controlar a ramificação e a profundidade de árvores de decisão.  
  
-   Especificar um valor de semente ou o tamanho do conjunto de controle interno usado na criação de modelo.  
  
 Os parâmetros fornecidos para cada algoritmo variam muito; para obter uma lista dos parâmetros que você pode definir para cada algoritmo, consulte os tópicos de referência técnica nesta seção: [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### Alterar um parâmetro de algoritmo  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse no tipo de modelo de mineração para o qual você quer ajustar o algoritmo e selecione **Definir Parâmetros de Algoritmo**.  
  
     A caixa de diálogo **Parâmetros do Algoritmo** é exibida.  
  
2.  Na coluna **Valor** , defina um novo valor para o algoritmo que você deseja alterar.  
  
     Se você não digitar um valor na coluna **Valor** , o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o valor de parâmetro padrão. A coluna **Intervalo** descreve os possíveis valores que você pode digitar.  
  
3.  Clique em **OK**.  
  
     O parâmetro de algoritmo será definido com o novo valor. A alteração de parâmetro não será refletida no modelo de mineração até que você processe o modelo novamente.  
  
### Exibir os parâmetros usados em um modelo existente  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma janela de consulta DMX.  
  
2.  Digite uma consulta como esta:  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  