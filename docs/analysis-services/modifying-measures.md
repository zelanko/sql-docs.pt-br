---
title: "Modificando medidas | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Modificando medidas
Você pode usar a propriedade **FormatString** para definir configurações de formatação que controlam como as medidas são exibidas aos usuários. Nesta tarefa, você especificará propriedades de formatação para as medidas moeda e porcentagem do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### Para modificar as medidas do cubo  
  
1.  Mude para a guia **Estrutura do Cubo** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], expanda o grupo de medidas **Vendas pela Internet** no painel **Medidas**, clique com o botão direito do mouse em **Quantidade de Pedidos** e clique em **Propriedades**.  
  
2.  Na janela Propriedades, clique no ícone de pino **Ocultar Automaticamente** para manter a janela Propriedades aberta.  
  
    É mais fácil alterar as propriedades de vários itens no cubo quando a janela Propriedades permanece aberta.  
  
3.  Na janela Propriedades, clique na lista **FormatString** e digite **#,#**.  
  
4.  Na barra de ferramentas da guia **Estrutura do Cubo** , clique no ícone **Mostrar Grade de Medidas** à esquerda.  
  
    A exibição das grades permite que você selecione várias medidas ao mesmo tempo.  
  
5.  Selecione as medidas a seguir. Você pode selecionar várias medidas clicando em cada uma enquanto mantém pressionada a tecla CTRL.  
  
    -   **Preço Unitário**  
  
    -   **Valor Ampliado**  
  
    -   **Valor de desconto**  
  
    -   **Custo Padrão do Produto**  
  
    -   **Custo Total do Produto**  
  
    -   **Valor das Vendas**  
  
    -   **Valor dos Impostos**  
  
    -   **Freight**  
  
6.  Na janela Propriedades, na lista **FormatString** , selecione **Moeda**.  
  
7.  Na lista suspensa na parte superior da janela Propriedades (logo abaixo da barra de título), selecione a medida **Percentual de Desconto no Preço Unitário** e **Percentual** na lista **FormatString**.  
  
8.  Na janela Propriedades, altere a propriedade **Name** da medida **Porcentagem de Desconto no Preço Unitário** para **Porcentagem de Desconto no Preço Unitário**.  
  
9. No painel **Medidas** , clique em **Valor dos Impostos** e altere o nome dessa medida para **Valor dos Impostos**.  
  
10. Na janela Propriedades, clique no ícone **Ocultar Automaticamente** para ocultar a janela Propriedades. Depois, clique em **Mostrar Árvore de Medidas** na barra de ferramentas da guia **Estrutura do Cubo** .  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## Próxima tarefa da lição  
[Modificando a dimensão Cliente](../analysis-services/modifying-the-customer-dimension.md)  
  
## Consulte também  
[Definir as dimensões do banco de dados](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[Configurar propriedades de medida](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  
