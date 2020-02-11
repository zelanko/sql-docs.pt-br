---
title: Atualizar a versão de um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- PerformUpgrade method
- custom data flow components [Integration Services], upgrading version
- data flow components [Integration Services], upgrading version
- upgrading data flow components [Integration Services]
ms.assetid: c2a298c6-01b3-4ad1-884d-6108165eb56e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 33ea6f845c323a858d1bd89318f2b8e07b734edd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896092"
---
# <a name="upgrading-the-version-of-a-data-flow-component"></a>Atualizando a versão de um componente de fluxo de dados
  Pacotes criados com uma versão mais antiga do seu componente podem conter metadados que não são mais válidos, como propriedades personalizadas cujo uso foi modificado em versões mais recentes do componente. É possível substituir o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> para atualizar os metadados salvos anteriormente em pacotes mais antigos, a fim de refletir as propriedades atuais do seu componente.  
  
> [!NOTE]  
>  Quando você compila novamente um componente personalizado para uma nova versão do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], não é necessário mudar o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> se as propriedades do componente não tiverem mudado.  
  
## <a name="example"></a>Exemplo  
 O exemplo seguinte contém o código da versão 2.0 de um componente de fluxo de dados fictício. O número da nova versão é definido na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. O componente tem uma propriedade que define como os valores numéricos que excedem um limite são tratados. Na versão 1.0 do componente fictício, essa propriedade era denominada `RaiseErrorOnInvalidValue` e aceitou um valor Booleano de verdadeiro ou falso. Na versão 2.0 do componente fictício, a propriedade foi renomeada para `InvalidValueHandling` e aceita um entre quatro valores possíveis de uma enumeração personalizada.  
  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> substituído no exemplo a seguir realiza as seguintes ações:  
  
-   Obtém a versão atual do componente.  
  
-   Obtém o valor da propriedade personalizada antiga.  
  
-   Remove a propriedade antiga da coleção de propriedades personalizadas.  
  
-   Define o valor da nova propriedade personalizada com base no valor da propriedade antiga, se possível.  
  
-   Define os metadados da versão para a versão atual do componente.  
  
> [!NOTE]  
>  O mecanismo de fluxo de dados passa seu próprio número de versão para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> no parâmetro *pipelineVersion*. Esse parâmetro não é útil na versão 1.0 do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], mas pode se tornar útil em versões subsequentes.  
  
 O código de exemplo usa somente os dois valores de enumeração, que mapeiam diretamente para os valores Booleanos anteriores para a propriedade personalizada. Os usuários podem selecionar os outros valores de enumeração disponíveis pela interface do usuário personalizada do componente, no Editor Avançado, ou programaticamente. Para obter informações sobre como exibir valores de enumeração para uma propriedade personalizada no Editor Avançado, consulte "Criando propriedades personalizadas" em [Métodos de tempo de design de um componente de fluxo de dados](design-time-methods-of-a-data-flow-component.md).  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(ComponentType:=ComponentType.Transform, CurrentVersion:=2)> _  
Public Class PerformUpgrade  
  Inherits PipelineComponent  
  
  ' Define the set of possible values for the new custom property.  
  Private Enum InvalidValueHandling  
    Ignore  
    FireInformation  
    FireWarning  
    FireError  
  End Enum  
  
  Public Overloads Overrides Sub PerformUpgrade(ByVal pipelineVersion As Integer)  
  
    ' Obtain the current component version from the attribute.  
    Dim componentAttribute As DtsPipelineComponentAttribute = _  
      CType(Attribute.GetCustomAttribute(Me.GetType, _  
      GetType(DtsPipelineComponentAttribute), False), _  
      DtsPipelineComponentAttribute)  
    Dim currentVersion As Integer = componentAttribute.CurrentVersion  
  
    ' If the component version saved in the package is less than  
    '  the current version, Version 2, perform the upgrade.  
    If ComponentMetaData.Version < currentVersion Then  
  
      ' Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
      ' and then remove the property from the custom property collection.  
      Dim oldValue As Boolean = False  
      Try  
        Dim oldProperty As IDTSCustomProperty100 = _  
          ComponentMetaData.CustomPropertyCollection("RaiseErrorOnInvalidValue")  
        oldValue = CType(oldProperty.Value, Boolean)  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue")  
      Catch ex As Exception  
        ' If the old custom property is not available, ignore the error.  
      End Try  
  
      ' Set the value of the new custom property, InvalidValueHandling,  
      '  by using the appropriate enumeration value.  
      Dim newProperty As IDTSCustomProperty100 = _  
        ComponentMetaData.CustomPropertyCollection("InvalidValueHandling")  
      If oldValue = True Then  
        newProperty.Value = InvalidValueHandling.FireError  
      Else  
        newProperty.Value = InvalidValueHandling.Ignore  
      End If  
  
    End If  
  
    ' Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
[DtsPipelineComponent(ComponentType = ComponentType.Transform, CurrentVersion = 2)]  
public class PerformUpgradeCS :  
  PipelineComponent  
  
  // Define the set of possible values for the new custom property.  
{  
  private enum InvalidValueHandling  
  {  
    Ignore,  
    FireInformation,  
    FireWarning,  
    FireError  
  };  
  
  public override void PerformUpgrade(int pipelineVersion)  
  {  
  
    // Obtain the current component version from the attribute.  
    DtsPipelineComponentAttribute componentAttribute =   
      (DtsPipelineComponentAttribute)Attribute.GetCustomAttribute(this.GetType(), typeof(DtsPipelineComponentAttribute), false);  
    int currentVersion = componentAttribute.CurrentVersion;  
  
    // If the component version saved in the package is less than  
    //  the current version, Version 2, perform the upgrade.  
    if (ComponentMetaData.Version < currentVersion)  
  
    // Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
    // and then remove the property from the custom property collection.  
    {  
      bool oldValue = false;  
      try  
      {  
        IDTSCustomProperty100 oldProperty =   
          ComponentMetaData.CustomPropertyCollection["RaiseErrorOnInvalidValue"];  
        oldValue = (bool)oldProperty.Value;  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue");  
      }  
      catch (Exception ex)  
      {  
        // If the old custom property is not available, ignore the error.  
      }  
  
      // Set the value of the new custom property, InvalidValueHandling,  
      //  by using the appropriate enumeration value.  
      IDTSCustomProperty100 newProperty =   
         ComponentMetaData.CustomPropertyCollection["InvalidValueHandling"];  
      if (oldValue == true)  
      {  
        newProperty.Value = InvalidValueHandling.FireError;  
      }  
      else  
      {  
        newProperty.Value = InvalidValueHandling.Ignore;  
      }  
  
    }  
  
    // Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion;  
  
  }  
  
}  
```  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
