---
title: Representação (tabela) de partição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b606cd63-755c-4ac0-b19b-95b5363afbdf
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cc8d3d1691b06e79da21f0ad173a570b58eff54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209876"
---
# <a name="partition-representation-tabular"></a>Representação de partição (tabular)
  Para fins operacionais, uma tabela pode ser dividida em subconjuntos diferentes de linhas que, quando combinados formam a tabela; cada um desses subconjuntos é uma partição da tabela.  
  
## <a name="partition-representation"></a>Representação de partição  
 Em termos de objetos AMO, uma representação de partição tem uma relação de mapeamento de um para um com <xref:Microsoft.AnalysisServices.Partition> e nenhum outro objeto AMO principal é necessário.  
  
### <a name="partition-in-amo"></a>Partição no AMO  
 Ao usar o AMO para gerenciar uma partição, você precisa localizar o grupo de medidas que representa a tabela de Modelo de tabela e trabalhar a partir daí.  
  
 O trecho de código a seguir mostra como adicionar uma partição a uma tabela de modelo de tabela existente.  
  
```  
  
private void AddPartition(  
                     AMO.Cube modelCube  
                  ,  AMO.DataSource newDatasource  
                  ,  string mgName  
                  ,  string newPartitionName  
                  , string partitionSelectStatement  
                  , Boolean processPartition  
             )  
{  
    mgName = mgName.Trim();  
    newPartitionName = newPartitionName.Trim();  
    partitionSelectStatement = partitionSelectStatement.Trim();  
    //Validate Input  
    if (string.IsNullOrEmpty(newPartitionName) || string.IsNullOrWhiteSpace(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (modelCube.MeasureGroups[mgName].Partitions.ContainsName(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name already defined. Duplicated names are not allowed"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (string.IsNullOrEmpty(partitionSelectStatement) || string.IsNullOrWhiteSpace(partitionSelectStatement))  
    {  
        MessageBox.Show(String.Format("Select statement cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    //Input validated  
    string partitionID = newPartitionName; //Using partition name as the ID  
    AMO.Partition currentPartition = new AMO.Partition(partitionID, partitionID);  
    currentPartition.StorageMode = AMO.StorageMode.InMemory;  
    currentPartition.ProcessingMode = AMO.ProcessingMode.Regular;  
    currentPartition.Source = new AMO.QueryBinding(newDatasource.ID, partitionSelectStatement);  
    modelCube.MeasureGroups[mgName].Partitions.Add(currentPartition);  
    try  
    {  
        modelCube.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        if (processPartition)  
        {  
            modelCube.MeasureGroups[mgName].Partitions[partitionID].Process(AMO.ProcessType.ProcessFull);  
            MessageBox.Show(String.Format("Partition successfully processed."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        }  
  
    }  
    catch (AMO.AmoException amoXp)  
    {  
        MessageBox.Show(String.Format("AMO exception accessing the server.\nError message: {0}", amoXp.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
    catch (Exception)  
    {  
        throw;  
    }  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>Exemplo de AMO2Tabular  
 No entanto, para compreender como usar o AMO para criar e manipular representações de partição, consulte o código-fonte do exemplo AMO para Tabela. O exemplo está disponível no Codeplex. Uma nota importante sobre o código: o código é fornecido apenas como um suporte aos conceitos lógicos explicados aqui; ele não deve ser usado em um ambiente de produção, nem para fins que não sejam pedagógicos.  
  
  
