---
title: Codificando e depurando o componente Script | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ff6c9814547a83439717f8a88d3bd52be80c4ca5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-component"></a>Codificando e depurando o componente Script
  No [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, o componente Script tem dois modos: modo de design de metadados e modo de design de código. Quando você abre o **Editor de transformação scripts**, o componente insere o modo de design de metadados, em que você configura metadados e definir propriedades do componente. Depois de definir as propriedades do componente Script e configurar a entrada e as saídas em modo de design de metadados, você pode alternar para o modo de design de código para gravar seu script personalizado. Para obter mais informações sobre o modo de design de metadados e modo de design de código, consulte [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Escrevendo o Script em modo de design de código  
  
### <a name="script-component-development-environment"></a>Ambiente de desenvolvimento do componente Script  
 Para escrever seu script, clique em **Editar Script** no **Script** página do **Editor de transformação scripts** para abrir o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE. O VSTA IDE inclui todos os recursos padrão do ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].NET, como o editor [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] codificado por cores, o IntelliSense e o Pesquisador de Objetos.  
  
 O código de Script é escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Especifique a linguagem de script definindo a **ScriptLanguage** propriedade o **Editor de transformação scripts**. Caso prefira usar outra linguagem de programação, você pode desenvolver um assembly personalizado na linguagem de sua escolha e chamar sua funcionalidade do código no componente Script.  
  
 O script criado no componente Script é armazenado na definição do pacote. Não há arquivo de script separado. Portanto, o uso do componente Script não afeta a implantação do pacote.  
  
> [!NOTE]  
>  Enquanto você projeta o pacote, o código de script é gravado temporariamente em um arquivo de projeto. Como o fato de armazenar informações confidenciais em um arquivo representa um potencial risco à segurança, recomendamos não incluir informações, como senhas, no código de script.  
  
 Por padrão, **Option Strict** está desabilitado no IDE.  
  
### <a name="script-component-project-structure"></a>Estrutura do projeto do componente Script  
 O poder do componente Script reside em poder gerar código de infraestrutura que reduz a quantidade de códigos que você deve gravar. Esse recurso se baseia no fato de que entradas e saídas e suas colunas e propriedades são fixadas e conhecidas com antecedência. Portanto, qualquer alteração subsequente que você faça nos metadados do componente poderá invalidar o código que você gravou. Isso causa erros de compilação durante a execução do pacote.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Itens e classes de projeto no projeto do componente Script  
 Quando você alterna para o modo de design de código, o VSTA IDE abre e exibe o **ScriptMain** item de projeto. O **ScriptMain** item de projeto contém o editável **ScriptMain** classe, que serve como a entrada de apontar para o script e que é onde você escreve seu código. Os elementos de código na classe variam dependendo da linguagem de programação que você selecionou para a tarefa Script.  
  
 O projeto de script contém dois itens de projeto somente leitura adicionais gerados automaticamente:  
  
-   O **ComponentWrapper** item de projeto contém três classes:  
  
    -   O **UserComponent** classe que herda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> e contém os métodos e propriedades que você usará para processar dados e interagir com o pacote. O **ScriptMain** classe herda o **UserComponent** classe.  
  
    -   Um **conexões** classe de coleção que contém referências às conexões selecionadas na página do Gerenciador de Conexão do Editor de transformação de Script.  
  
    -   Um **variáveis** classe de coleção que contém referências a variáveis inseridas no **ReadOnlyVariable** e **ReadWriteVariables** propriedades no **Script** página do **Editor de transformação scripts**.  
  
-   O **BufferWrapper** item de projeto contém uma classe que herda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada e saída configurada no **entradas e saídas** página do **Editor de transformação scripts**. Cada uma dessas classes contém propriedades de acessador digitadas que correspondem às colunas de entrada e saída configuradas e os buffers de fluxo de dados que contêm as colunas.  
  
 Para obter informações sobre como usar esses objetos, métodos e propriedades, consulte [Noções básicas sobre o modelo de objeto do componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md). Para obter informações sobre como usar os métodos e propriedades dessas classes em um tipo específico de componente Script, consulte a seção [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Os tópicos de exemplo também contêm exemplos de código completos.  
  
 Quando você configura o componente Script como uma transformação, o **ScriptMain** item de projeto contém o seguinte código gerado automaticamente. O modelo de código também fornece uma visão geral do componente Script e informações adicionais sobre como recuperar e manipular objetos SSIS, como variáveis, eventos e conexões.  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>Itens de projeto adicionais no projeto do componente Script  
 O projeto do componente Script pode incluir itens que não seja o padrão **ScriptMain** item. Você pode adicionar classes, módulos, arquivos de código e pastas ao projeto, e você pode usar pastas para organizar grupos de itens.  
  
 Todos os itens que você adiciona persistem dentro do pacote.  
  
#### <a name="references-in-the-script-component-project"></a>Referências no projeto do componente Script  
 Você pode adicionar referências a assemblies gerenciados clicando com o projeto da tarefa Script no **Explorador de projeto**e, em seguida, clicando em **adicionar referência**. Para obter mais informações, consulte [referenciando outros Assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Você pode exibir as referências do projeto no VSTA IDE em **exibição de classe** ou **Explorador de projeto**. Abrir uma dessas janelas do **exibição** menu. Você pode adicionar uma nova referência do **projeto** menu de **Explorador de projeto**, ou de **exibição de classe**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interagindo com o pacote no componente Script  
 O script personalizado que você grava no componente Script pode acessar e usar variáveis e gerenciadores de conexões do pacote que os contém através de acessadores de tipo mais acentuado nas classes base geradas automaticamente. Contudo, você deve configurar as variáveis e os gerenciadores de conexões antes de digitar o modo de design de código, se quiser disponibilizá-los para seu script. Você também pode gerar eventos e executar log do código do componente Script.  
  
 Os itens de projeto gerados automaticamente no projeto do componente Script fornecem os seguintes objetos, métodos e propriedades para interagir com o pacote.  
  
|Recurso do Pacote|Método de Acesso|  
|---------------------|-------------------|  
|Variáveis|Usar as propriedades de acessador nomeadas e digitadas no **variáveis** classe de coleção no **ComponentWrapper** exposta por meio de item de projeto, o **variáveis** propriedade do **ScriptMain** classe.<br /><br /> O **PreExecute** método pode acessar somente as variáveis somente leitura. O **PostExecute** método pode acessar somente leitura e variáveis de leitura/gravação.|  
|Conexões|Usar as propriedades de acessador nomeadas e digitadas no **conexões** classe de coleção no **ComponentWrapper** exposta por meio de item de projeto, o **conexões** propriedade do **ScriptMain** classe.|  
|Eventos|Acionar eventos usando o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> propriedade o **ScriptMain** classe e o **incêndio\<X >** métodos do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interface.|  
|Log|Executar o registro em log usando o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método o **ScriptMain** classe.|  
  
## <a name="debugging-the-script-component"></a>Depurando o componente Script  
 Para depurar o código no seu componente Script, defina pelo menos um ponto de interrupção no código e, depois, feche o VSTA IDE para executar o pacote no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Quando a execução do pacote insere o componente Script, o VSTA IDE é reaberto e exibe seu código em modo somente leitura. Depois que a execução atingir seu ponto de interrupção, você poderá examinar valores de variáveis e passar pelo código restante.  
  
> [!NOTE]  
>  Você não pode depurar um componente Script quando executa-o como parte de um pacote filho que é executado a partir de uma tarefa Executar Pacote. Nessas circunstâncias, os pontos de interrupção definidos no componente Script no pacote filho são desconsiderados. Você pode depurar o pacote filho normalmente, executando-o separadamente.  
  
> [!NOTE]  
>  Quando você depura um pacote que contém vários componentes Script, o depurador depura um componente Script. O sistema poderá depurar outro componente Script se o depurador for concluído, como no caso de um contêiner Loop Foreach ou Loop For.  
  
 Você também pode monitorar a execução do componente Script usando os métodos seguintes:  
  
-   Interrompa a execução e exiba uma mensagem modal usando o **MessageBox. show** método o **System** namespace. (Remova esse código após concluir o processo de depuração).  
  
-   Gere eventos para mensagens informativas, advertências e erros. Os métodos FireInformation, FireWarning e FireError a descrição do evento de exibição no Visual Studio **saída** janela. No entanto, o método FireProgress, o método Write e método console. WriteLine não exibe todas as informações de **saída** janela. Mensagens de evento FireProgress aparecem no **andamento** guia de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Para obter mais informações, consulte [gerando eventos no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md).  
  
-   Eventos de log ou mensagens definidas pelo usuário para provedores de log habilitados. Para obter mais informações, consulte [log no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md).  
  
 Se você quiser apenas para examinar a saída de um componente Script configurado como uma fonte ou como uma transformação, sem salvar os dados para um destino, você pode interromper o fluxo de dados com um [transformação contagem de linhas](../../../integration-services/data-flow/transformations/row-count-transformation.md) e anexar um visualizador de dados para a saída do componente Script. Para obter informações sobre os visualizadores de dados, consulte [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Para obter mais informações sobre como codificar o componente Script, consulte os tópicos seguintes nesta seção.  
  
 [Noções básicas sobre o modelo de objeto do componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Explica como usar os objetos, métodos e propriedades disponíveis no componente Script.  
  
 [Referenciando outros Assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Explica como referenciar objetos da biblioteca de classes [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] no componente Script.  
  
 [Simulando uma saída de erro para o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Explica como simular uma saída de erro para linhas que geram erros durante o processamento pelo componente Script.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [problemas de instalação e configuração de VSTA para instalações de SSIS 2008 e R2](http://go.microsoft.com/fwlink/?LinkId=215661), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  

