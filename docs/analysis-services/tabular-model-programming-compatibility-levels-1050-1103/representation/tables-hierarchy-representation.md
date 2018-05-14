---
title: Representação de hierarquia (tabela) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ed1232a991ccdefbd9cae614698400cfe639492
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="tables---hierarchy-representation"></a>Tabelas - representação de hierarquia
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Em modelos de tabela, uma hierarquia é o caminho de navegação de um atributo para outro com base em valores selecionados pelo usuário.  
  
## <a name="hierarchy-representation"></a>Representação de hierarquia  
  
### <a name="hierarchy-in-amo"></a>Hierarquia no AMO  
 Ao usar o AMO para gerenciar uma tabela de modelo de tabela, há correspondência de objeto um para um em uma hierarquia no AMO. Uma hierarquia é representada pelo objeto <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
 O trecho de código a seguir mostra como adicionar uma hierarquia a um modelo de tabela existente. O código supõe que você tenha um objeto de banco de dados de AMO, newDatabase e um objeto de cubo AMO, modelCube.  
  
```  
  
private void addHierarchy(  
                    AMO.Database newDatabase  
                 ,  AMO.Cube modelCube  
                 ,  string tableName  
                 ,  string hierarchyName  
                 ,  string levelsText  
             )  
{  
    //Validate input  
    if (string.IsNullOrEmpty(hierarchyName) || string.IsNullOrEmpty(levelsText))  
    {  
        MessageBox.Show(String.Format("Hierarchy Name or Layout must be provided."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
  
    if (!overwriteHierarchy.Checked && newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
    {  
        MessageBox.Show(String.Format("Hierarchy already exists.\nGive a new name or enable overwriting"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
  
    try  
    {  
        if (newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
        {  
            //Hierarchy exists... deleting it to write it later  
            newDatabase.Dimensions[tableName].Hierarchies.Remove(hierarchyName, true);  
            newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
        }  
        AMO.Hierarchy currentHierarchy = newDatabase.Dimensions[tableName].Hierarchies.Add(hierarchyName, hierarchyName);  
        currentHierarchy.AllMemberName = string.Format("(All of {0})", hierarchyName);  
        //Parse hierarchyLayout  
        using (StringReader levels = new StringReader(levelsText))  
        {  
            //Each line:  
            //  must come with: The columnId of the attribute in the dimension --> this represents the SourceAttributeID  
            //  optional: A display name for the Level (if this argument doesn't come the default is the SourceAttributeID)  
            string line;  
            while ((line = levels.ReadLine()) != null)  
            {  
                if (string.IsNullOrEmpty(line) || string.IsNullOrWhiteSpace(line)) continue;  
                line = line.Trim();  
                string[] hierarchyData = line.Split(',');  
                if (string.IsNullOrEmpty(hierarchyData[0])) continue; //first argument cannot be empty or blank,   
                                                                      //assume is a blank line and ignore it  
                string levelSourceAttributeID = hierarchyData[0].Trim();  
                string levelID = (hierarchyData.Length > 1 && !string.IsNullOrEmpty(hierarchyData[1])) ? hierarchyData[1].Trim() : levelSourceAttributeID;  
                currentHierarchy.Levels.Add(levelID).SourceAttributeID = levelSourceAttributeID;  
            }  
        }  
        newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
  
    }  
    catch (Exception ex)  
    {  
        MessageBox.Show(String.Format("Error creating hierarchy [{0}].\nError message: {1}", newHierarchyName.Text, ex.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        if (newDatabase.Dimensions[tableName].Hierarchies.Contains(hierarchyName))  
        {  
            //Hierarchy was created but exception prevented complete hierarchy to be written... deleting incomplete hierarchy  
            newDatabase.Dimensions[tableName].Hierarchies.Remove(hierarchyName, true);  
            newDatabase.Dimensions[tableName].Update(AMO.UpdateOptions.AlterDependents);  
        }  
  
    }  
    newDatabase.Dimensions[tableName].Process(AMO.ProcessType.ProcessFull);  
    modelCube.MeasureGroups[tableName].Process(AMO.ProcessType.ProcessFull);  
}  
  
```  
  
  
