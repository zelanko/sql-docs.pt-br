---
title: 'A lição suplementar tutorial do Analysis Services: hierarquias desbalanceadas | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc5a2164576e2e6142d8835dad6f6c114b7a9c5b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lição suplementar - hierarquias desbalanceadas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição suplementar, você resolver um problema comum quando dinamização em hierarquias que contêm valores em branco (membros) em diferentes níveis. Por exemplo, uma organização onde um gerente de alto nível tem os gerentes departamentais e não gerentes como subordinados diretos. Ou hierarquias geográficas composto por país-região-cidades, onde algumas cidades não têm um pai de estado ou província, como Washington D.C., a cidade do Vaticano. Quando uma hierarquia tem membros em branco, geralmente desce a níveis diferentes ou desbalanceados.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

Modelos de tabela no nível de compatibilidade 1400 têm adicional **ocultar membros** propriedade para hierarquias. O **padrão** configuração pressupõe que não existem membros em branco em qualquer nível. O **ocultar membros em branco** configuração exclui membros em branco da hierarquia quando adicionada a uma tabela dinâmica ou relatório.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este artigo lição suplementar faz parte de um tutorial de modelagem de tabela. Antes de executar as tarefas nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído. 

Se você criou o projeto de vendas pela Internet AW como parte do tutorial, o modelo ainda não contém dados ou hierarquias desbalanceadas. Para concluir esta lição suplementar, você precisa primeiro criar o problema adicionando algumas tabelas adicionais, criar relações, colunas calculadas, uma medida e uma nova hierarquia da organização. Essa parte leva cerca de 15 minutos. Em seguida, você pode resolvê-lo em apenas alguns minutos.  

## <a name="add-tables-and-objects"></a>Adicionar tabelas e objetos
  
### <a name="to-add-new-tables-to-your-model"></a>Para adicionar novas tabelas a seu modelo
  
1.  No Gerenciador de modelos tabulares, expanda **fontes de dados**, em seguida, clique com botão direito sua conexão > **importar novas tabelas**.
  
2.  No navegador, selecione **DimEmployee** e **FactResellerSales**e, em seguida, clique em **Okey**.

3.  No Editor de consultas, clique em **importação**

4.  Crie a seguinte [relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | Tabela 1           | Coluna       | Direção do filtro   | Tabela 2     | Coluna      | Ativa |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Padrão            | DimDate     | Data        | Sim    |
    | FactResellerSales | DueDate      | Padrão            | DimDate     | Data        | não     |
    | FactResellerSales | ShipDateKey  | Padrão            | DimDate     | Data        | não     |
    | FactResellerSales | ProductKey   | Padrão            | DimProduct  | ProductKey  | Sim    |
    | FactResellerSales | EmployeeKey  | Para ambas as tabelas | DimEmployee | EmployeeKey | Sim    |

5. No **DimEmployee** de tabela, crie a seguinte [colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **Caminho** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Nível 1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  No **DimEmployee** de tabela, crie um [hierarquia](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) chamado **organização**. Adicione a seguintes colunas na ordem: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  No **FactResellerSales** de tabela, crie a seguinte [medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) para abrir o Excel e criar automaticamente uma tabela dinâmica.

9.  Em **PivotTable Fields**, adicione o **organização** hierarquia da **DimEmployee** tabela **linhas**e o  **ResellerTotalSales** medir a partir de **FactResellerSales** tabela **valores**.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Como você pode ver na tabela dinâmica, a hierarquia exibe linhas que são irregulares. Há muitas linhas em que os membros em branco são mostrados.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Para corrigir a hierarquia desbalanceada, definindo os membros de ocultar propriedade

1.  Em **Gerenciador de modelos tabulares**, expanda **tabelas** > **DimEmployee** > **hierarquias**  >  **Organização**.

2.  Em **propriedades** > **ocultar membros**, selecione **ocultar membros em branco**. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  No Excel, atualize a tabela dinâmica. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Agora que parece muito melhor!

## <a name="see-also"></a>Consulte também   
[Lição 9: criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Lição suplementar - segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lição suplementar - linhas de detalhes](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
