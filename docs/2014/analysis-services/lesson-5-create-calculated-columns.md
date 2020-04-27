---
title: 'Lição 6: criar colunas calculadas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58ba761f3e32f13ddcf81dc9875057195298c705
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078559"
---
# <a name="lesson-6-create-calculated-columns"></a>Lição 6: Criar colunas calculadas
  Nesta lição, você criará novos dados no modelo adicionando colunas calculadas. Uma coluna calculada se baseia nos dados que já existem no modelo. Para saber mais, consulte [Colunas calculadas &#40;SSAS Tabular&#41;](tabular-models/ssas-calculated-columns.md).  
  
 Você criará cinco novas colunas calculadas em três tabelas diferentes. As etapas são ligeiramente diferentes para cada tarefa. O objetivo disso é mostrar que há vários modos de criar novas colunas, renomeá-las e colocá-las em vários locais em uma tabela.  
  
 Tempo estimado para conclusão desta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 5: Criar relações](lesson-4-create-relationships.md).  
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Criar uma coluna calculada Month Calendar na tabela Date  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , aponte para **Exibição de Modelo**e clique em **Exibição de Dados**.  
  
     Colunas calculadas só podem ser criadas usando o designer de modelos na exibição de dados.  
  
2.  No designer de modelos, clique na tabela **Data** (guia).  
  
3.  Clique com o botão direito do mouse na coluna **calendário trimestre** e clique em **Inserir coluna**.  
  
     Uma nova coluna chamada **CalculatedColumn1** é inserida à esquerda da coluna **calendário Quarter** .  
  
4.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir. O Preenchimento Automático ajuda você a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
     Os valores são populados para todas as linhas na coluna calculada. Se você rolar para baixo na tabela, você verá que linhas podem ter valores diferentes para esta coluna, com base nos dados que estão em cada linha.  
  
    > [!NOTE]  
    >  Se você receber um erro, verifique se os nomes de coluna na fórmula correspondem aos nomes de coluna alterados na [Lição 3: Renomear colunas](rename-columns.md).  
  
5.  Renomeie esta `Month Calendar`coluna como.  
  
 A coluna calculada Month Calendar fornece um nome classificável para o mês.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Criar uma coluna calculada Day of Week na tabela Date  
  
1.  Com a tabela **Date** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
     Uma nova coluna é adicionada à extrema direita da tabela.  
  
2.  Na barra de fórmulas, digite a seguinte fórmula:  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Renomeie a `Day of Week`coluna para.  
  
4.  Clique no título de coluna e arraste a coluna entre as colunas **Day Name** e **Day of Month** .  
  
    > [!TIP]  
    >  A movimentação das colunas na tabela facilita a navegação.  
  
 A coluna calculada Day of Week fornece um nome classificável para o dia de semana.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Criar uma coluna calculada Product Subcategory Name na tabela Product  
  
1.  No designer de modelos, selecione a tabela **Product** .  
  
2.  Role a tela para a extrema direita da tabela. Observe que a coluna mais à direita é denominada **Adicionar Coluna** (em itálico), clique no título de coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a `Product Subcategory Name`coluna para.  
  
 A coluna calculada Product Subcategory Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Subcategory Name na tabela Product Subcategory. Hierarquias não podem abranger mais de uma tabela. Você criará hierarquias posteriormente na lição 7.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Criar uma coluna calculada Product Category Name na tabela Product  
  
1.  Com a tabela **Product** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
2.  Na barra de fórmulas, digite a seguinte fórmula:  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Renomeie a `Product Category Name`coluna para.  
  
 A coluna calculada Product Category Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Category Name na tabela Product Category. Hierarquias não podem abranger mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Criar uma coluna calculada Margin na tabela Internet Sales  
  
1.  No designer de modelos, selecione a tabela **Internet Sales** .  
  
2.  Adicione uma nova coluna.  
  
3.  Na barra de fórmulas, digite a seguinte fórmula:  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a `Margin`coluna para.  
  
5.  Arraste a coluna entre as colunas **Sales Amount** e **Tax Amt** .  
  
 A coluna calculada Margin é usada para analisar margens de lucro para cada linha (produto).  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar esta lição, vá para a próxima lição: [Lição 7: Criar medidas](lesson-6-create-measures.md).  
  
  
