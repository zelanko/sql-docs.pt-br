---
title: Validar um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ReinitializeMetaData method
- Validate method
- component validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- data flow components [Integration Services], validating
- validation [Integration Services]
ms.assetid: 1a7d5925-b387-4e31-af7f-c7f3c5151040
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e58de07841aeba956e6bc8d552b14237a31b515e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968816"
---
# <a name="validating-a-data-flow-component"></a>Validando um componente de fluxo de dados
  O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> é fornecido para impedir a execução de um componente que não está configurado corretamente. Utilize esse método para verificar se um componente possui o número esperado de objetos de entrada e saída, se as propriedades personalizadas do componente possuem valores aceitáveis e se há conexões especificadas, caso necessário. Utilize esse método também para verificar se as colunas nas coleções de entrada e saída possuem os tipos de dados corretos e se o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType> de cada coluna está definido adequadamente para o componente. A implementação da classe base ajuda no processo de validação pois verifica a coleção de colunas de entrada do componente e se cada coluna da coleção se refere a uma coluna do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100> do componente upstream.  
  
## <a name="validate-method"></a>Método Validate  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> é chamado repetidamente quando um componente é editado no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Você pode fornecer comentários ao designer e a usuários do componente através do valor de retorno de enumeração <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> e postando avisos e erros. A enumeração <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> contém três valores que indicam vários estágios da falha e um quarto valor, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISVALID>, que indica se o componente foi configurado corretamente e se está pronto para ser executado.  
  
 O valor <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> indica que existe um erro no <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>, e que o componente pode reparar os erros. Se um componente encontrar um erro de metadados que possa reparar, não deverá corrigir o erro no método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> não deverá ser modificado durante a validação. Em vez disso, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> deve retornar apenas <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> e o componente deve reparar o erro em uma chamada para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>, conforme descrito posteriormente nessa seção.  
  
 O valor <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISBROKEN> indica que o componente tem um erro que pode ser retificado editando o componente no designer. O erro costuma ser causado por uma propriedade personalizada ou uma conexão exigeida que não foi especificada ou foi definida incorretamente.  
  
 O valor de erro final é <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISCORRUPT>, que indica que o componente descobriu erros que só devem ocorrer quando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> é modificada diretamente, através da edição do pacote XML ou do uso do modelo de objeto. Por exemplo, esse tipo de erro ocorre quando um componente adiciona uma única entrada, mas a validação descobre que existe mais de uma entrada no <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>. Erros que geram esse valor retornado só podem ser reparados através da redefinição do componente utilizando o botão **Redefinir** na caixa de diálogo **Editor Avançado**.  
  
 Além de retornar valores de erro, componentes fornecem comentários postando avisos ou erros durante a validação. Os métodos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> fornecem esse mecanismo. Quando esses métodos são chamados, esses eventos são postados na janela **Lista de Erros** do [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Desenvolvedores de componente podem fornecer comentários diretos a usuários sobre os erros que ocorreram e, se apropriado, como corrigi-los.  
  
 O exemplo de código a seguir mostra uma implementação substituída de <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    bool pbCancel = false;  
  
    // Validate that there is one input.  
    if (ComponentMetaData.InputCollection.Count != 1)  
    {  
    ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, out pbCancel);  
    return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Validate that the UserName custom property is set.  
    if (ComponentMetaData.CustomPropertyCollection["UserName"].Value == null || ((string)ComponentMetaData.CustomPropertyCollection["UserName"].Value).Length == 0)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISBROKEN;  
    }  
  
    // Validate that there is one output.  
    if (ComponentMetaData.OutputCollection.Count != 1)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Let the base class verify that the input column reflects the output   
    // of the upstream component.  
    return base.Validate();  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
  
 Dim pbCancel As Boolean = False  
  
 ' Validate that there is one input.  
 If Not (ComponentMetaData.InputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Validate that the UserName custom property is set.  
 If ComponentMetaData.CustomPropertyCollection("UserName").Value Is Nothing OrElse CType(ComponentMetaData.CustomPropertyCollection("UserName").Value, String).Length = 0 Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISBROKEN   
 End If   
  
 ' Validate that there is one output.  
 If Not (ComponentMetaData.OutputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Let the base class verify that the input column reflects the output   
 ' of the upstream component.  
  
 Return MyBase.Validate   
  
End Function  
```  
  
## <a name="reinitializemetadata-method"></a>Método ReinitializeMetaData  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> é chamado pelo [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer sempre que você edita um componente que retorna <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> do seu método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>. Componentes devem conter código que detecta e corrige os problemas identificados pelo componente durante a validação.  
  
 O exemplo a seguir mostra um componente que detecta problemas durante a validação e corrige-os no método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>.  
  
```csharp  
private bool areInputColumnsValid = true;  
public override DTSValidationStatus Validate()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
    bool Cancel = false;  
    foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
    {  
        try  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
        }  
        catch  
        {  
            ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, out Cancel);  
            areInputColumnsValid = false;  
            return DTSValidationStatus.VS_NEEDSNEWMETADATA;  
        }  
    }  
  
    return DTSValidationStatus.VS_ISVALID;  
}  
public override void ReinitializeMetaData()  
{  
    if (!areInputColumnsValid)  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection[0];  
        IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
        foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
  
            if (vColumn == null)  
                input.InputColumnCollection.RemoveObjectByID(column.ID);  
        }  
        areInputColumnsValid = true;  
    }  
}  
```  
  
```vb  
Private areInputColumnsValid As Boolean = True   
  
Public  Overrides Function Validate() As DTSValidationStatus   
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
 Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
 Dim Cancel As Boolean = False   
 For Each column As IDTSInputColumn100 In input.InputColumnCollection   
   Try   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
   Catch   
     ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, Cancel)   
     areInputColumnsValid = False   
     Return DTSValidationStatus.VS_NEEDSNEWMETADATA   
   End Try   
 Next   
 Return DTSValidationStatus.VS_ISVALID   
End Function   
  
Public  Overrides Sub ReinitializeMetaData()   
 If Not areInputColumnsValid Then   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
   Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
   For Each column As IDTSInputColumn100 In input.InputColumnCollection   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
     If vColumn Is Nothing Then   
       input.InputColumnCollection.RemoveObjectByID(column.ID)   
     End If   
   Next   
   areInputColumnsValid = True   
 End If   
End Sub  
```  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
