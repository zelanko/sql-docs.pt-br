---
title: Programando objetos de mineração de dados AMO | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: d27f58b9-91be-449c-8403-439aa6dd1ff9
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 62ef444d7fa112267a4a272553834e24fe5b0df9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117538"
---
# <a name="programming-amo-data-mining-objects"></a>Programando objetos de mineração de dados AMO
  A programação de objetos de mineração de dados usando AMO é simples e direta. A primeira etapa é criar o modelo de estrutura de dados para dar suporte ao projeto de mineração. Em seguida, você cria o modelo de mineração que dá suporte ao algoritmo de mineração que deseja usar para prever ou para localizar os relacionamentos despercebidos subjacentes aos seus dados. Com o seu projeto de mineração criado (incluindo a estrutura e os algoritmos), você poderá processar os modelos de mineração para obter os modelos treinados que usará mais tarde ao consultar e fazer previsões a partir do aplicativo cliente.  
  
 Você deve se lembrar de que o AMO não foi feito para consultas; ele foi criado para o gerenciamento e para a administração das suas estruturas e modelos de mineração. Para consultar os dados, use [desenvolvendo com ADOMD.NET](../adomd-net/developing-with-adomd-net.md).  
  
 Este tópico contém as seguintes seções:  
  
-   [Objetos MiningStructure](#MiningStructure)  
  
-   [Objetos MiningModel](#MiningModel)  
  
##  <a name="MiningStructure"></a> Objetos MiningStructure  
 Uma estrutura de mineração é a definição da estrutura de dados usada para criar todos os modelos de mineração. Uma estrutura de mineração contém uma ligação a uma exibição de fonte de dados definida no banco de dados e contém definições para todas as colunas que participam dos modelos de mineração. Uma estrutura de mineração pode ter mais de um modelo de mineração.  
  
 A criação de um objeto <xref:Microsoft.AnalysisServices.MiningStructure> exige as seguintes etapas:  
  
1.  Criar o objeto <xref:Microsoft.AnalysisServices.MiningStructure> e preencha os atributos básicos. Os atributos básicos incluem o nome do objeto, a ID do objeto (identificação interna) e a ligação da fonte de dados.  
  
2.  Crie colunas para o modelo. As colunas podem ser escalares ou definições de tabela.  
  
     Cada coluna precisa de um nome e de ID interna, de um tipo, de uma definição de conteúdo e de uma associação.  
  
3.  Atualizar o objeto <xref:Microsoft.AnalysisServices.MiningStructure> no servidor por meio do método Update do objeto.  
  
     As estruturas de mineração podem ser processadas, e quando isso acontece, os modelos de mineração filhos são processados ou retreinados.  
  
 O código de exemplo a seguir cria uma estrutura de mineração para a previsão de vendas em uma série temporal. Antes de executar o código de exemplo, verifique se o banco de dados *db*passado como parâmetro para `CreateSalesForecastingMiningStructure`, contém em `db.DataSourceViews[0]` uma referência para o modo de exibição *dbo.vTimeSeries* no [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]banco de dados de exemplo.  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a> Objetos MiningModel  
 Um modelo de mineração é um repositório para todas as colunas e definições de coluna que serão usadas em um algoritmo de mineração.  
  
 A criação de um objeto <xref:Microsoft.AnalysisServices.MiningModel> exige as seguintes etapas:  
  
1.  Criar o objeto <xref:Microsoft.AnalysisServices.MiningModel> e preencha os atributos básicos.  
  
     Os atributos básicos incluem o nome do objeto, a ID do objeto (identificação interna) e a especificação do algoritmo de mineração.  
  
2.  Adicione as colunas do modelo de mineração. Um das colunas deve ser definida como a chave do caso.  
  
3.  Atualizar o objeto <xref:Microsoft.AnalysisServices.MiningModel> no servidor por meio do método Update do objeto.  
  
     Os objetos <xref:Microsoft.AnalysisServices.MiningModel> podem ser processados de forma independente de outros modelos no <xref:Microsoft.AnalysisServices.MiningStructure> pai.  
  
 O código de exemplo a seguir cria um modelo de previsão MTS baseado na estrutura de mineração "Forecasting Sales Structure":  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Classes fundamentais AMO](amo-fundamental-classes.md)   
 [Introdução às Classes AMO](amo-classes-introduction.md)   
 [Classes de mineração de dados AMO](amo-data-mining-classes.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  