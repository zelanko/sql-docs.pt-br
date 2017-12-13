---
title: Adicione dados de exemplo para um modelo DirectQuery no modo de Design | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1af1e823-85aa-4319-a93f-98b35f7c7322
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 962cadeac40c4cd450265d6c617a2bdcf1afa9ac
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="add-sample-data-to-a-directquery-model-in-design-mode"></a>Adicionar dados de exemplo a um modelo DirectQuery no Modo de Design
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]No modo DirectQuery, as partições de tabela são usadas para criar subconjuntos de dados de exemplo usados durante o design do modelo, ou criar alternativas de uma exibição de dados completo.
 
 Quando você implanta um modelo de tabela do DirectQuery, somente uma partição é permitida por tabela, e essa partição obrigatoriamente deve ser a exibição de dados completa. Qualquer partição adicional é um substituto da exibição de dados completa ou dados de exemplo. Neste tópico, vamos descrever como criar uma partição de exemplo, com um subconjunto de dados.
 
 Por padrão, ao criar um modelo de tabela no modo DirectQuery no SSDT, o banco de dados de trabalho do modelo não contém dados. Há uma partição padrão para cada tabela, e essa partição direciona todas as consultas para a fonte de dados. 
  
No entanto, você pode adicionar uma quantidade menor de dados de exemplo ao banco de dados de trabalho do modelo para uso em tempo de design. Os dados de exemplo são especificados por meio de uma consulta em uma partição de exemplo usada somente durante o design. Eles são armazenados em cache na memória com o modelo. Isso ajudará a validar as decisões de modelagem sem afetar a fonte de dados. Você pode testar suas decisões de modelagem com o conjunto de dados de exemplo quando usar o recurso **Analisar no Excel** no SSDT (SQL Server Data Tools) ou em outros aplicativos cliente que se conectam ao seu banco de dados de espaço de trabalho.  
  
> [!TIP]  
>  Mesmo no modo DirectQuery em um modelo vazio, você sempre poderá exibir um pequeno conjunto de linhas interno para cada tabela. Em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique em **Tabela** > **Propriedades da Tabela** para exibir o conjunto de dados de 50 linhas.  
  
## <a name="create-a-sample-partition"></a>Criar uma partição de exemplo
 Essas instruções são para modelos de tabela criados ou atualizados para o nível de compatibilidade 1200 ou superior. Modelos em níveis de compatibilidade inferiores usam propriedades diferentes para obter dados armazenados em cache. Consulte [Habilitar o modo DirectQuery no SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md) para obter descrições de propriedade.  
  
1.  No SQL Server Data Tools, na Exibição de Diagrama ou de Dados, clique em uma tabela de fatos para abrir sua página de propriedades. Tabelas de fatos fornecem dados agregados, numéricos e medidas em seu modelo. Você pode ter mais de um.  
  
2.  Clique em **Tabela** > **Propriedades** para abrir a caixa de diálogo Gerenciamento de Partição.  
  
    Observe que a partição padrão é **(consulta direta) \<nome da tabela >**. Esta é a exibição de dados completa. Não exclua essa partição. Essa partição será usada quando o modelo for implantado.  
  
4.  Selecione a partição e clique em **Copiar**.  

    Isso cria uma cópia da partição padrão; no entanto, essa cópia conterá dados de exemplo que você especificar em uma consulta. Por exemplo:
  
     ![ssas_tabularproject_copypartition](../../analysis-services/tabular-models/media/ssas-tabularproject-copypartition.jpg "ssas_tabularproject_copypartition")  
  
5.  Selecione a partição copiada e clique no botão **Editor de Consultas SQL** para adicionar um filtro. Reduza o tamanho dos dados de exemplo ao criar seu modelo. Por exemplo, se você selecionou **FactInternetSales** de AdventureWorksDW, o filtro poderá ser parecido com este:  
  
    ```  
    SELECT [dbo].[FactInternetSales].* FROM [dbo].[FactInternetSales]  
    JOIN DimSalesTerritory as ST  
    ON ST.SalesTerritoryKey = FactInternetSales.SalesTerritoryKey  
    WHERE ST.SalesTerritoryGroup='North America';  
    ```  
  
6.  Clique em **Validar** para verificar erros de sintaxe.  
  
     Observe que, no modo DirectQuery, além dos botões **Novo** , **Copiar**, e **Excluir** na caixa de diálogo Partições, também há um botão de alternância que lê, alternativamente, **Definir como Exemplo** ou **Definir como DirectQuery**.  
  
     Apenas uma partição pode ser a partição DirectQuery. Você pode controlar isso selecionando qualquer partição definida para a tabela e clicando em **Definir como Exemplo**.  
  
7.  Processe a tabela.  
  


  
  
