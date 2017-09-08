---
title: Definindo um cubo | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bbc83e63aabb254d4b7393f5672e0fca426a707b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-2---defining-a-cube"></a>Lição 2-2-definir um cubo
O Assistente para Cubos ajuda-o a definir os grupos de medidas e dimensões de um cubo. Na tarefa a seguir, você usará o Assistente para Cubos para criar um cubo.  
  
### <a name="to-define-a-cube-and-its-properties"></a>Para definir um cubo e suas propriedades  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Cubos**e clique em **Novo Cubo**. O Assistente para Cubos é exibido.  
  
2.  Na página **Bem-vindo ao Assistente para Cubos** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Criação** , verifique se a opção **Usar tabelas existentes** está selecionada e clique em **Avançar**.  
  
4.  Na página **Selecionar Tabelas de Grupos de Medidas** , verifique se a exibição da fonte de dados **Adventure Works DW 2012** está selecionada.  
  
5.  Clique em **Sugerir** para que o assistente para cubos sugira as tabelas a serem usadas na criação do grupo de medidas.  
  
    O assistente examina as tabelas e sugere **InternetSales** como uma tabela do grupo de medidas. As tabelas do grupo de medidas, também denominadas tabelas de fatos, contêm medidas que lhe interessam; por exemplo, o número de unidades vendidas.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Selecionar Medidas** , examine as medidas selecionadas no grupo de medidas **Vendas pela Internet** e desmarque as caixas de seleção das seguintes medidas:  
  
    -   **Chave da Promoção**  
  
    -   **Chave da Moeda**  
  
    -   **Chave da Região de Vendas**  
  
    -   **Número de Revisão**  
  
    Por padrão, o assistente seleciona como medidas todas as colunas numéricas da tabela de fatos que não estão vinculadas a dimensões. Porém, essas quatro colunas não são medidas reais. As três primeiras são valores de chave que vinculam a tabela de fatos às tabelas de dimensão que não são usadas na versão inicial deste cubo.  
  
8.  Clique em **Avançar**.  
  
9. Na página **Selecionar Dimensões Existentes** , verifique se a dimensão **Data** criada anteriormente está selecionada e clique em **Avançar**.  
  
10. Na página **Selecionar Novas Dimensões** , selecione as novas dimensões que serão criadas. Para fazer isso, verifique se as caixas de seleção **Cliente**, **Geografia**e **Produto** estão marcadas e desmarque a caixa de seleção **InternetSales** .  
  
11. Clique em **Avançar**.  
  
12. Na página **Concluindo o Assistente** , altere o nome do cubo para **Tutorial do Analysis Services**. No painel Visualização, você pode ver o grupo de medidas **InternetSales** e suas medidas. É possível ver também as dimensões **Data**, **Cliente** e **Produto** .  
  
13. Clique em **Concluir** para concluir o assistente.  
  
    No Gerenciador de Soluções, no projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é exibido na pasta **Cubos** e as dimensões de banco de dados Cliente e Produto são exibidas na pasta **Dimensões** . Além disso, no centro do ambiente de desenvolvimento, a guia Estrutura do Cubo exibe o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
14. Na barra de ferramentas da guia Estrutura do Cubo, altere o nível **Zoom** para 50%, de forma que fique mais fácil ver as dimensões e tabelas de fatos no cubo. Observe que a tabela de fato é amarela e as tabelas de dimensão são azuis.  
  
15. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Adicionando atributos em dimensões](../analysis-services/lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>Consulte também  
[Cubos em modelos multidimensionais](../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
[Dimensões em modelos multidimensionais](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
  

