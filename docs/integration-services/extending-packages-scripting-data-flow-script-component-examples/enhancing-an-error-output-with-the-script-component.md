---
title: Aprimorando uma saída de erro com o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba095c6aa132a816dc63377d0b04f559df6a6853
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297075"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Aprimorando uma saída de erro com o componente Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Por padrão as duas colunas extras em uma saída de erro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ErrorCode e ErrorColumn, só contêm códigos numéricos que representam um número de erro e a ID da coluna na qual o erro aconteceu. Esses valores numéricos podem ser de pouca utilidade sem a descrição do erro e o nome da coluna correspondentes.  
  
 Este tópico descreve como adicionar a descrição de erro e o nome da coluna a dados de saída de erro existentes no fluxo de dados usando o componente Script. O exemplo adiciona a descrição de erro que corresponde a um código de erro específico e predefinido do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> da interface do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponível através da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> do componente Script. Em seguida, o exemplo adiciona o nome da coluna que corresponde à ID de linhagem capturada usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> da mesma interface.  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo demonstrado aqui usa um componente Script configurado como uma transformação para adicionar a descrição de erro e o nome da coluna a dados de saída de erro existentes no fluxo de dados.  
  
 Para obter mais informações sobre como configurar o componente Script para uso como uma transformação no fluxo de dados, consulte [Criando uma transformação síncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) e [Criando uma transformação assíncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Antes de criar o novo componente Script, configure um componente upstream no fluxo de dados para redirecionar linhas para sua saída de erro quando um erro ou truncamento ocorrer. Por motivo de teste, você pode configurar um componente de forma a assegurar que os erros ocorram – por exemplo, configurando uma transformação Pesquisa entre duas tabelas em que a pesquisa vai falhar.  
  
2.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
3.  Conecte a saída de erro do componente upstream ao novo componente Script.  
  
4.  Abra o **Editor de Transformação Scripts** e, na página **Script**, para a propriedade **ScriptLanguage**, selecione a linguagem de script.  
  
5.  Clique em **Editar Script** para abrir o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) e adicionar o código de exemplo mostrado abaixo.  
  
6.  Feche o VSTA.  
  
7.  No Editor de Transformação Scripts, na página **Colunas de Entrada**, selecione as colunas ErrorCode e ErrorColumn.  
  
8.  Na página **Entradas e saídas**, adicione duas novas colunas.  
  
    -   Adicione uma nova coluna de saída do tipo **String** chamada **ErrorDescription**. Aumente o comprimento padrão da coluna nova para 255 para suportar mensagens longas.  
  
    -   Adicione outra nova coluna de saída do tipo **String** chamada **ColumnName**. Aumente o tamanho padrão da nova coluna para 255 para dar suporte a mensagens longas.  
  
9. Feche o **Editor de Transformação Scripts**.  
  
10. Anexe a saída do componente Script a um destino satisfatório. Um destino de arquivo simples é o mais fácil de configurar para testar ad hoc.  
  
11. Execute o pacote.  

```vb
Public Class ScriptMain      ' VB
    Inherits UserComponent
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)

        Row.ErrorDescription = _
            Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)

        Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)

        If componentMetaData130 IsNot Nothing Then

            If Row.ErrorColumn = 0 Then
                ' 0 means no specific column is identified by ErrorColumn, this time.
                Row.ColumnName = "Check the row for a violation of a foreign key constraint."
            ELSE If Row.ErrorColumn = -1 Then
                ' -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables."
            Else
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)
            End If
        End If
    End Sub
End Class
```

```csharp
public class ScriptMain:      // C#
    UserComponent
{
    public override void Input0_ProcessInputRow(Input0Buffer Row)
    {
        Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);

        var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;
        if (componentMetaData130 != null)
        {
            // 0 means no specific column is identified by ErrorColumn, this time.
            if (Row.ErrorColumn == 0)
            {
                Row.ColumnName = "Check the row for a violation of a foreign key constraint.";
            }
            // -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
            else if (Row.ErrorColumn == -1)
            {
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables.";
            }
            else
            {
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);
            }
        }
    }
}
```

## <a name="see-also"></a>Consulte Também  
 [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)   
 [Usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Criar uma transformação síncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
