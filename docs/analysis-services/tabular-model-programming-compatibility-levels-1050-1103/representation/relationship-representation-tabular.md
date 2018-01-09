---
title: "Representação de relação (tabela) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 86a5eff8-4e07-444b-ac15-5695f09aa105
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c0fef50d7a63d51955dcc523e07957c237d530ff
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="relationship-representation-tabular"></a>Representação de relação (de tabela)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Uma relação é uma conexão entre duas tabelas de dados. A relação estabelece como os dados nas duas tabelas devem ser correlacionados.  
  
 Consulte [representação de relação (Tabular)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md) para obter uma explicação detalhada sobre como criar e manipular a representação de relação.  
  
## <a name="relationship-representation"></a>Representação de relação  
 Em modelos de tabela, podem ser definidas várias relações entre duas tabelas. Quando são definidas várias relações entre duas tabelas, somente uma pode ser definida como a relação padrão para o modelo e é chamada de relação Ativa; todas as outras relações são chamadas de Inativas.  
  
### <a name="relationship-in-amo"></a>Relação no AMO  
 Em termos de objetos AMO, todas as relações inativas têm uma representação de uma relação de mapeamento um para um com o <xref:Microsoft.AnalysisServices.Relationship> e nenhum outro objeto AMO principal é exigido; para a relação ativa outros requisitos existem e um mapeamento para o <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> também é exigido.  
  
 Os trechos de códigos a seguir mostram como criar uma relação em modelos de tabela, como ativar uma relação e como definir uma chave primária em uma tabela (além de "RowNumber"). Para criar uma relação ativa, uma chave primária precisa ser definida na tabela de chave primária - PKTableName - da relação (o lado um da relação). O exemplo mostrado aqui cria a chave primária no PKColumnName se nenhuma chave primária tiver sido definida nesta coluna. Podem ser criadas relações inativas sem a necessidade de ter uma chave primária na coluna de chave primária.  
  
```  
  
private Boolean createRelationship(string PKTableName, string PKColumnName, string MVTableName, string MVColumnName, AMO.Database tabularDb, string cubeName, Boolean forceActive)  
{  
    //verify input parameters  
    if(     string.IsNullOrEmpty(PKTableName) || string.IsNullOrWhiteSpace(PKTableName)  
        ||  string.IsNullOrEmpty(PKColumnName) || string.IsNullOrWhiteSpace(PKColumnName)  
        ||  string.IsNullOrEmpty(MVTableName) || string.IsNullOrWhiteSpace(MVTableName)  
        ||  string.IsNullOrEmpty(MVColumnName) || string.IsNullOrWhiteSpace(MVColumnName)  
        ||  (tabularDb == null)  
        ) return false;  
    if(!tabularDb.Dimensions.ContainsName(PKTableName) || !tabularDb.Dimensions.ContainsName(MVTableName)) return false;  
    if(!tabularDb.Dimensions[PKTableName].Attributes.ContainsName(PKColumnName) || !tabularDb.Dimensions[MVTableName].Attributes.ContainsName(MVColumnName)) return false;  
  
    //Verify underlying cube structure  
    if (!tabularDb.Cubes[cubeName].Dimensions.ContainsName(PKTableName) || !tabularDb.Cubes[cubeName].Dimensions.ContainsName(MVTableName)) return false; //Should return an exception!!  
    if (!tabularDb.Cubes[cubeName].MeasureGroups.ContainsName(PKTableName) || !tabularDb.Cubes[cubeName].MeasureGroups.ContainsName(MVTableName)) return false; //Should return an exception!!  
  
    //Make sure PKTableName.PKColumnName  is set as PK ==> <attribute>.usage == AMO.AttributeUsage.Key  
    if (tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].Usage != AMO.AttributeUsage.Key)  
    {  
        //... here we are 'fixing', if there is an issue with PKTableName.PKColumnName not beeing the PK of the table  
        setPKColumn(tabularDb, PKTableName, PKColumnName);  
    }  
  
    //Terminology note:   
    // -   the many side of the relationship is named the From end in AMO  
    // -   the PK side of the relationship in named the To end in AMO  
    //  
    //It seems relationships flow FROM the many side of the relationship in TO the primary key side of the relationship in AMO  
    //              
    //Verify the relationship we are creating does not exist, regardless of name.  
    //if it exists, return true (no need to recreate it)  
    //if it doesn't exists it will be created after this validation  
  
    //   
    foreach (AMO.Relationship currentRelationship in tabularDb.Dimensions[MVTableName].Relationships)  
    {  
        if ((currentRelationship.FromRelationshipEnd.Attributes[0].AttributeID == MVColumnName)  
            && (currentRelationship.ToRelationshipEnd.DimensionID == PKTableName)  
            && (currentRelationship.ToRelationshipEnd.Attributes[0].AttributeID == PKColumnName))  
        {  
            if (forceActive)  
            {  
                //Activate the relationship   
                setActiveRelationship(tabularDb.Cubes[cubeName], MVTableName, MVColumnName, PKTableName, currentRelationship.ID);  
                //Update server with changes made here  
                tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.CreateOrReplace);  
                tabularDb.Cubes[cubeName].MeasureGroups[MVTableName].Process(AMO.ProcessType.ProcessFull);  
            }  
            return true;  
        }  
    }  
  
    //A relationship like the one to be created does not exist; ergo, let's create it:  
  
    //First, create the INACTIVE relationship definitions in the MultipleValues end of the relationship  
    #region define unique name for relationship  
    string newRelationshipID = string.Format("Relationship _{0}_{1}_ to _{2}_{3}_", MVTableName, MVColumnName, PKTableName, PKColumnName);  
    int rootLen = newRelationshipID.Length;  
    for (int i = 0; tabularDb.Dimensions[MVTableName].Relationships.Contains(newRelationshipID); )  
    {  
        newRelationshipID = string.Format("{0}_{1,8:0}", newRelationshipID.Substring(0, rootLen), i);  
    }  
    #endregion  
    AMO.Relationship newRelationship = tabularDb.Dimensions[MVTableName].Relationships.Add(newRelationshipID);  
  
    newRelationship.FromRelationshipEnd.DimensionID = MVTableName;  
    newRelationship.FromRelationshipEnd.Attributes.Add(MVColumnName);  
    newRelationship.FromRelationshipEnd.Multiplicity = AMO.Multiplicity.Many;  
    newRelationship.FromRelationshipEnd.Role = string.Empty;  
    newRelationship.ToRelationshipEnd.DimensionID = PKTableName;  
    newRelationship.ToRelationshipEnd.Attributes.Add(PKColumnName);  
    newRelationship.ToRelationshipEnd.Multiplicity = AMO.Multiplicity.One;  
    newRelationship.ToRelationshipEnd.Role = string.Empty;  
  
    //Update server to create relationship  
    tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    tabularDb.Dimensions[MVTableName].Process(AMO.ProcessType.ProcessDefault);  
    tabularDb.Dimensions[PKTableName].Process(AMO.ProcessType.ProcessDefault);  
  
    //Second, activate the relationship if relationship is to be set as the active relationship: 'forceActive==true'  
    //... an inactive relationship needs only to be created on the dimensions object  
    if (forceActive)  
    {  
        //Activate the relationship   
        setActiveRelationship(tabularDb.Cubes[cubeName], MVTableName, MVColumnName, PKTableName, newRelationshipID);                  
    }             
    return true;  
}  
  
private void setActiveRelationship(AMO.Cube currentCube, string MVTableName, string MVColumnName, string PKTableName, string relationshipID)  
{  
    if (!currentCube.MeasureGroups.Contains(MVTableName))  
    {  
        throw new AMO.AmoException(string.Format("Cube [{0}] does not contain Measure Group [{1}]\nError activating relationship [{2}]: [{4}] <--- [{1}].[{3}]"  
                                                , currentCube.Name, MVTableName, relationshipID, MVColumnName, PKTableName));  
    }  
    AMO.MeasureGroup currentMG = currentCube.MeasureGroups[MVTableName];  
  
    if (!currentMG.Dimensions.Contains(PKTableName))  
    {  
        AMO.ReferenceMeasureGroupDimension newReferenceMGDim = new AMO.ReferenceMeasureGroupDimension();  
        newReferenceMGDim.CubeDimensionID = PKTableName;  
        newReferenceMGDim.IntermediateCubeDimensionID = MVTableName;  
        newReferenceMGDim.IntermediateGranularityAttributeID = MVColumnName;  
        newReferenceMGDim.Materialization = AMO.ReferenceDimensionMaterialization.Regular;  
        newReferenceMGDim.RelationshipID = relationshipID;  
        foreach (AMO.CubeAttribute PKAttribute in currentCube.Dimensions[PKTableName].Attributes)  
        {  
            AMO.MeasureGroupAttribute PKMGAttribute = newReferenceMGDim.Attributes.Add(PKAttribute.AttributeID);  
            OleDbType PKMGAttributeType = PKAttribute.Attribute.KeyColumns[0].DataType;  
            PKMGAttribute.KeyColumns.Add(new AMO.DataItem(PKTableName, PKAttribute.AttributeID, PKMGAttributeType));  
            PKMGAttribute.KeyColumns[0].Source = new AMO.ColumnBinding(PKTableName, PKAttribute.AttributeID);  
        }  
        currentMG.Dimensions.Add(newReferenceMGDim);  
  
        AMO.ValidationErrorCollection errors = new AMO.ValidationErrorCollection();  
  
        newReferenceMGDim.Validate(errors, true);  
        if (errors.Count > 0)  
        {  
            StringBuilder errorMessages = new StringBuilder();  
            foreach (AMO.ValidationError err in errors)  
            {  
                errorMessages.AppendLine(string.Format("At {2}: # {0} : {1}", err.ErrorCode, err.FullErrorText, err.Source));  
            }  
            throw new AMO.AmoException(errorMessages.ToString());  
        }  
        //Update changes in the server  
        currentMG.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.CreateOrReplace);  
    }  
    else  
    {  
        AMO.ReferenceMeasureGroupDimension currentReferenceMGDim = (AMO.ReferenceMeasureGroupDimension)currentMG.Dimensions[PKTableName];  
        currentReferenceMGDim.RelationshipID = relationshipID;  
        currentReferenceMGDim.IntermediateGranularityAttributeID = MVColumnName;  
        //Update changes in the server  
        currentMG.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    }  
    //process MG to activate relationship  
    currentMG.Process(AMO.ProcessType.ProcessFull);  
  
}  
  
private void setPKColumn(AMO.Database tabularDb, string PKTableName, string PKColumnName)  
{  
        //Find all 'unwanted' Key attributes, remove their Key definitions and include the attributes in the ["RowNumber"].AttributeRelationships  
        foreach (AMO.DimensionAttribute currentDimAttribute in tabularDb.Dimensions[PKTableName].Attributes)  
        {  
            if ((currentDimAttribute.Usage == AMO.AttributeUsage.Key) && (currentDimAttribute.ID != PKColumnName))  
            {  
                currentDimAttribute.Usage = AMO.AttributeUsage.Regular;  
                if (currentDimAttribute.ID != "RowNumber")  
                {  
                    currentDimAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Preserve;  
                    currentDimAttribute.AttributeRelationships.Clear();  
                    if (!tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.ContainsName(currentDimAttribute.ID))  
                    {  
                        AMO.DimensionAttribute currentAttribute = tabularDb.Dimensions[PKTableName].Attributes[currentDimAttribute.ID];  
                        AMO.AttributeRelationship currentAttributeRelationship = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.Add(currentAttribute.ID);  
                        currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
                    }  
                    tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships[currentDimAttribute.ID].Cardinality = AMO.Cardinality.Many;  
                }  
            }  
        }  
  
        //Remove PKColumnName from ["RowNumber"].AttributeRelationships  
        int PKAtribRelationshipPosition = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.IndexOf(PKColumnName);  
        if (PKAtribRelationshipPosition != -1) tabularDb.Dimensions[PKTableName].Attributes["RowNumber"].AttributeRelationships.RemoveAt(PKAtribRelationshipPosition, true);  
  
        //Define PKColumnName as Key and add ["RowNumber"] to PKColumnName.AttributeRelationships with cardinality of One  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].Usage = AMO.AttributeUsage.Key;  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].KeyColumns[0].NullProcessing = AMO.NullProcessing.Error;  
        if (!tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships.ContainsName("RowNumber"))  
        {  
            AMO.DimensionAttribute currentAttribute = tabularDb.Dimensions[PKTableName].Attributes["RowNumber"];  
            AMO.AttributeRelationship currentAttributeRelationship = tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships.Add(currentAttribute.ID);  
            currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
        }  
        tabularDb.Dimensions[PKTableName].Attributes[PKColumnName].AttributeRelationships["RowNumber"].Cardinality = AMO.Cardinality.One;  
  
        //Update Table before going creating the relationship  
        tabularDb.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        tabularDb.Dimensions[PKTableName].Process(AMO.ProcessType.ProcessDefault);                
  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>Exemplo de AMO2Tabular  
 No entanto, para compreender como usar o AMO para criar e manipular representações de relação, consulte o código-fonte do exemplo AMO para Tabela. O exemplo está disponível no Codeplex. Uma nota importante sobre o código: o código é fornecido apenas como um suporte aos conceitos lógicos explicados aqui; ele não deve ser usado em um ambiente de produção, nem para fins que não sejam pedagógicos.  
  
  
