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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042300"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lição suplementar – hierarquias desbalanceadas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição suplementar, você resolver um problema comum ao dinamizar hierarquias que contêm valores em branco (membros) em diferentes níveis. Por exemplo, uma organização em que um gerente de alto nível tem tanto gerentes departamentais quanto não gerentes como subordinados diretos. Ou então, hierarquias geográficas compostas por país-região-cidades, onde algumas cidades não têm um estado ou província pai, como Washington D.C. e cidade do Vaticano. Quando uma hierarquia tem membros em branco, ela geralmente desce a níveis diferentes ou desbalanceados.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

Modelos de tabela no nível de compatibilidade 1400 têm adicional **ocultar membros** propriedade para hierarquias. O **padrão** configuração pressupõe que não existem membros em branco em qualquer nível. O **ocultar membros em branco** configuração exclui membros em branco da hierarquia quando adicionada a uma tabela dinâmica ou relatório.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este artigo de lição suplementar faz parte de um tutorial de modelagem de tabela. Antes de executar as tarefas nesta lição suplementar, você deve ter concluído todas as lições anteriores ou ter um projeto de modelo de exemplo Adventure Works Internet Sales concluído. 

Se você tiver criado o projeto de vendas pela Internet AW como parte do tutorial, seu modelo ainda não contém nenhum dado ou hierarquias desbalanceadas. Para concluir esta lição suplementar, você precisa primeiro criar o problema adicionando algumas tabelas adicionais, criar relações, colunas calculadas, uma medida e uma nova hierarquia da organização. Essa parte leva cerca de 15 minutos. Em seguida, você pode resolvê-la em apenas alguns minutos.  

## <a name="add-tables-and-objects"></a>Adicionar tabelas e objetos
  
### <a name="to-add-new-tables-to-your-model"></a>Para adicionar novas tabelas para seu modelo
  
1.  No Gerenciador de modelos tabulares, expanda **fontes de dados**, em seguida, clique com botão direito sua conexão > **importar novas tabelas**.
  
2.  No navegador, selecione **DimEmployee** e **FactResellerSales**e, em seguida, clique em **Okey**.

3.  No Editor de consultas, clique em **importação**

4.  Crie a seguinte [relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | Tabela 1           | coluna       | Direção do filtro   | Tabela 2     | coluna      | Ativa |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Padrão            | DimDate     | data        | Sim    |
    | FactResellerSales | DueDate      | Padrão            | DimDate     | data        | não     |
    | FactResellerSales | ShipDateKey  | Padrão            | DimDate     | data        | não     |
    | FactResellerSales | ProductKey   | Padrão            | DimProduct  | ProductKey  | Sim    |
    | FactResellerSales | EmployeeKey  | Para ambas as tabelas | DimEmployee | EmployeeKey | Sim    |

5. No **DimEmployee** da tabela, crie a seguinte [colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

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

6.  No **DimEmployee** da tabela, criar um [hierarquia](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) denominada **organização**. Adicione as seguintes colunas em ordem: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  No **FactResellerSales** da tabela, crie a seguinte [medida](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) para abrir o Excel e criar automaticamente uma tabela dinâmica.

9.  No **PivotTable Fields**, adicionar o **organização** hierarquia da **DimEmployee** tabela **linhas**e o  **ResellerTotalSales** medida de **FactResellerSales** tabela **valores**.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Como você pode ver na tabela dinâmica, a hierarquia exibe linhas que são irregulares. Há muitas linhas em que os membros em branco são mostrados.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Para corrigir a hierarquia desbalanceada definindo propriedade ocultar membros

1.  Na **Gerenciador de modelos tabulares**, expanda **tabelas** > **DimEmployee** > **hierarquias**  >  **Organização**.

2.  Na **propriedades** > **ocultar membros**, selecione **ocultar membros em branco**. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  No Excel, atualiza a tabela dinâmica. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Agora que se parece muito melhor!

## <a name="see-also"></a>Consulte também   
[Lição 9: criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Lição suplementar - segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lição suplementar - linhas de detalhes](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
