---
title: 'Lição 6: Criar colunas calculadas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adc7b7bf3335c8c9c7530d18f4d553492cfe9e1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728629"
---
# <a name="lesson-6-create-calculated-columns"></a>Lição 6: Criar colunas calculadas
  Nesta lição, você criará novos dados no modelo adicionando colunas calculadas. Uma coluna calculada se baseia nos dados que já existem no modelo. Para saber mais, consulte [Colunas calculadas &#40;SSAS Tabular&#41;](tabular-models/ssas-calculated-columns.md).  
  
 Você criará cinco novas colunas calculadas em três tabelas diferentes. As etapas são ligeiramente diferentes para cada tarefa. O objetivo disso é mostrar que há vários modos de criar novas colunas, renomeá-las e colocá-las em vários locais em uma tabela.  
  
 Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 5: Criar relações](lesson-4-create-relationships.md).  
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Criar uma coluna calculada Month Calendar na tabela Date  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo**, aponte para **Exibição de Modelo** e clique em **Exibição de Dados**.  
  
     Colunas calculadas só podem ser criadas usando o designer de modelos na exibição de dados.  
  
2.  No designer de modelos, clique na tabela **Data** (guia).  
  
3.  Clique com botão direito do **trimestre do calendário** coluna e clique **Inserir coluna**.  
  
     Uma nova coluna chamada **CalculatedColumn1** é inserida à esquerda do **trimestre do calendário** coluna.  
  
4.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir. O recurso Preenchimento Automático ajuda a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
     Os valores são preenchidos em todas as linhas da coluna calculada. Se você rolar para baixo na tabela, verá que as linhas podem ter valores diferentes para essa coluna baseados nos dados que estão em cada linha.  
  
    > [!NOTE]  
    >  Se você receber um erro, verifique se os nomes de coluna na fórmula correspondem aos nomes de coluna alterados em [lição 3: Renomear colunas](rename-columns.md).  
  
5.  Renomeie esta coluna como `Month Calendar`.  
  
 A coluna calculada Month Calendar fornece um nome classificável para o mês.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Criar uma coluna calculada Day of Week na tabela Date  
  
1.  Com a tabela **Date** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
     Uma nova coluna é adicionada à extrema direita da tabela.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Renomeie a coluna para `Day of Week`.  
  
4.  Clique no título de coluna e arraste a coluna entre as colunas **Day Name** e **Day of Month** .  
  
    > [!TIP]  
    >  A movimentação das colunas na tabela facilita a navegação.  
  
 A coluna calculada Day of Week fornece um nome classificável para o dia de semana.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Criar uma coluna calculada Product Subcategory Name na tabela Product  
  
1.  No designer de modelos, selecione a tabela **Product** .  
  
2.  Role a tela para a extrema direita da tabela. Observe que a coluna mais à direita é chamada **Adicionar Coluna** (em itálico); clique no título de coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a coluna para `Product Subcategory Name`.  
  
 A coluna calculada Product Subcategory Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Subcategory Name na tabela Product Subcategory. As hierarquias não podem ultrapassar mais de uma tabela. Você criará hierarquias posteriormente na lição 7.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Criar uma coluna calculada Product Category Name na tabela Product  
  
1.  Com a tabela **Product** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Renomeie a coluna para `Product Category Name`.  
  
 A coluna calculada Product Category Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Category Name na tabela Product Category. As hierarquias não podem ultrapassar mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Criar uma coluna calculada Margin na tabela Internet Sales  
  
1.  No designer de modelos, selecione a tabela **Internet Sales** .  
  
2.  Adicione uma nova coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a coluna para `Margin`.  
  
5.  Arraste a coluna entre as colunas **Sales Amount** e **Tax Amt** .  
  
 A coluna calculada Margin é usada para analisar margens de lucro para cada linha (produto).  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar esta lição, vá para a próxima lição: [Lição 7: Criar medidas](lesson-6-create-measures.md).  
  
  
