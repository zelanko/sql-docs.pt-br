---
title: Implementando metadados externos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8e43702349bae9dd5f3eb89bb6454fb62b05816
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169183"
---
# <a name="implementing-external-metadata"></a>Implementando metadados externos
  Quando um componente é desconectado de sua fonte de dados, você pode validar as colunas nas coleções de colunas de entrada e saída com base nas colunas da fonte de dados externa por meio da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100>. Essa interface permite que você mantenha um instantâneo das colunas na fonte de dados externa e as mapeie para as colunas da coleção de colunas de entrada e saída do componente.  
  
 A implementação de colunas de metadados externos adiciona uma camada de sobrecarga e complexidade ao desenvolvimento do componente, já que você deve fazer a manutenção e a validação em uma coleção de colunas adicionais. Entretanto, a capacidade de evitar viagens dispendiosas de ida e volta ao servidor para validação pode tornar esse trabalho de desenvolvimento compensador.  
  
## <a name="populating-external-metadata-columns"></a>Preenchendo colunas de metadados externos  
 Normalmente, colunas de metadados externas são adicionadas à coleção quando a coluna de entrada ou de saída correspondente é criada. Novas colunas são criadas chamando-se o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A>. As propriedades da coluna são definidas para corresponder à fonte de dados externa.  
  
 A coluna de metadados externos é mapeada para a coluna de entrada e saída correspondente atribuindo-se a ID da coluna de metadados externos à propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> da coluna de entrada e saída. Isto permite que você localize com facilidade a coluna de metadados externos para uma coluna de entrada ou saída específica usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> da coleção.  
  
 O exemplo a seguir mostra como criar uma coluna de metadados externos e mapear a coluna para uma coluna de saída ao definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A>.  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>Validando com colunas de metadados externos  
 A validação requer etapas adicionais para componentes que mantêm uma coleção de colunas de metadados externos, porque você deve validar com base em uma coleção adicional de colunas. A validação pode ser dividida em validação conectada ou desconectada.  
  
### <a name="connected-validation"></a>Validação conectada  
 Quando um componente é conectado a uma fonte de dados externa, as colunas nas coleções de entrada ou saída são verificadas diretamente na fonte de dados externa. Adicionalmente, as colunas na coleção de metadados externos devem ser validadas. Isso é necessário porque a coleção de metadados externos pode ser modificada por meio do **Editor Avançado** no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e as alterações feitas à coleção não são detectáveis. Portanto, quando conectados, os componentes devem verificar se as colunas da coleção de colunas de metadados externos continuam refletindo as colunas da fonte de dados externa.  
  
 Você pode optar por ocultar a coleção de metadados externos na **Editor Avançado** definindo o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A> propriedade da coleção para `false`. Entretanto, esse procedimento também oculta a guia **Mapeamento de Coluna** do editor, a qual permite que os usuários mapeiem as colunas da coleção de entrada ou saída para as colunas da coleção de colunas de metadados externos. A definição desta propriedade como `false` não impede que os desenvolvedores modifiquem programaticamente a coleção, mas, efetivamente, fornece um nível de proteção para a coleção de colunas de metadados externos de um componente que é utilizado exclusivamente no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="disconnected-validation"></a>Validação desconectada  
 Quando um componente é desconectado de uma fonte de dados externa, a validação é simplificada porque as colunas da coleção de entrada ou saída são verificadas diretamente com base nas colunas da coleção de metadados externos e não com base na fonte externa. Um componente deve executar a validação desconectada quando a conexão com sua fonte de dados externa não tiver sido estabelecida ou quando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> for `false`.  
  
 O exemplo de código a seguir demonstra uma implementação de um componente que executa validação com base em sua coleção de colunas de metadados externos.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../../data-flow/data-flow.md)  
  
  
