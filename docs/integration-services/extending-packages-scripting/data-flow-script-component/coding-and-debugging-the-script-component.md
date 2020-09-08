---
description: Codificando e depurando o componente Script
title: Codificar e depurar o componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 763f3abaff3d2b12d6a03b0d0dabb43f9111a910
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480958"
---
# <a name="coding-and-debugging-the-script-component"></a>Codificando e depurando o componente Script

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  No [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, o componente Script tem dois modos: modo de design de metadados e modo de design de código. Quando você abre o **Editor de Transformação Scripts**, o componente digita o modo de design de metadados no qual você configura metadados e define propriedades do componente. Depois de definir as propriedades do componente Script e configurar a entrada e as saídas em modo de design de metadados, você pode alternar para o modo de design de código para gravar seu script personalizado. Para obter mais informações sobre o modo de design de metadados e modo de design de código, consulte [Configurando o componente Script no Editor de Componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Escrevendo o Script em modo de design de código  
  
### <a name="script-component-development-environment"></a>Ambiente de desenvolvimento do componente Script  
 Para gravar o script, clique em **Editar Script** na página **Script** do **Editor de Transformação Scripts** para abrir o IDE do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VSTA ([!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications). O VSTA IDE inclui todos os recursos padrão do ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].NET, como o editor [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] codificado por cores, o IntelliSense e o Pesquisador de Objetos.  
  
 O código de Script é escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Você especifica a linguagem de script configurando a propriedade **ScriptLanguage** no **Editor de Transformação Scripts**. Caso prefira usar outra linguagem de programação, você pode desenvolver um assembly personalizado na linguagem de sua escolha e chamar sua funcionalidade do código no componente Script.  
  
 O script criado no componente Script é armazenado na definição do pacote. Não há arquivo de script separado. Portanto, o uso do componente Script não afeta a implantação do pacote.  
  
> [!NOTE]  
>  Enquanto você projeta o pacote, o código de script é gravado temporariamente em um arquivo de projeto. Como o fato de armazenar informações confidenciais em um arquivo representa um potencial risco à segurança, recomendamos não incluir informações, como senhas, no código de script.  
  
 Por padrão, **Option Strict** fica desabilitado no IDE.  
  
### <a name="script-component-project-structure"></a>Estrutura do projeto do componente Script  
 O poder do componente Script reside em poder gerar código de infraestrutura que reduz a quantidade de códigos que você deve gravar. Esse recurso se baseia no fato de que entradas e saídas e suas colunas e propriedades são fixadas e conhecidas com antecedência. Portanto, qualquer alteração subsequente que você faça nos metadados do componente poderá invalidar o código que você gravou. Isso causa erros de compilação durante a execução do pacote.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Itens e classes de projeto no projeto do componente Script  
 Quando você muda para o modo de design de código, o VSTA IDE abre e exibe o item de projeto **ScriptMain**. O item de projeto **ScriptMain** contém a classe **ScriptMain** editável, que serve como ponto de entrada para o script e como local de gravação do seu código. Os elementos de código na classe variam dependendo da linguagem de programação que você selecionou para a tarefa Script.  
  
 O projeto de script contém dois itens de projeto somente leitura adicionais gerados automaticamente:  
  
-   O item de projeto **ComponentWrapper** contém três classes:  
  
    -   A classe **UserComponent**, que herda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> e contém os métodos e propriedades que você vai usar para processar dados e interagir com o pacote. A classe **ScriptMain** herda a classe **UserComponent**.  
  
    -   Uma classe de coleção **Connections**, que contém referências às conexões selecionadas na página Gerenciador de Conexões do Editor de Transformação Scripts.  
  
    -   Uma classe de coleção **Variables** que contém referências às variáveis inseridas nas propriedades **ReadOnlyVariable** e **ReadWriteVariables** na página **Script** do **Editor de Transformação Scripts**.  
  
-   O item de projeto **BufferWrapper** contém uma classe que herda do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada e saída configurada na página **Entradas e Saídas** do **Editor de Transformação Scripts**. Cada uma dessas classes contém propriedades de acessador digitadas que correspondem às colunas de entrada e saída configuradas e os buffers de fluxo de dados que contêm as colunas.  
  
 Para obter mais informações sobre como usar esses objetos, métodos e propriedades, consulte [Compreender o Component Object Model do Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md). Para obter informações sobre como usar os métodos e propriedades dessas classes em um tipo específico de componente Script, consulte a seção [Exemplos adicionais de componente de script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Os tópicos de exemplo também contêm exemplos de código completos.  
  
 Quando você configura o componente Script como uma transformação, o item de projeto **ScriptMain** contém o seguinte código gerado automaticamente. O modelo de código também fornece uma visão geral do componente Script e informações adicionais sobre como recuperar e manipular objetos SSIS, como variáveis, eventos e conexões.  
  
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
 O projeto do componente Script pode incluir itens diferentes do item **ScriptMain** padrão. Você pode adicionar classes, módulos, arquivos de código e pastas ao projeto, e você pode usar pastas para organizar grupos de itens.  
  
 Todos os itens que você adiciona persistem dentro do pacote.  
  
#### <a name="references-in-the-script-component-project"></a>Referências no projeto do componente Script  
 Você pode adicionar referências a assemblies gerenciados clicando com o botão direito do mouse no projeto da tarefa Script no **Explorador de Projeto** e clicando em **Adicionar Referência**. Para obter mais informações, consulte [Referenciar outros assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Você pode exibir as referências do projeto no IDE VSTA no **Modo de Exibição de Classe** ou no **Explorador de Projeto**. É possível abrir qualquer uma dessas janelas no menu **Exibir**. Você pode adicionar uma referência nova no menu **Projeto**, de **Explorador de Projeto** ou de **Modo de Exibição de Classe**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interagindo com o pacote no componente Script  
 O script personalizado que você grava no componente Script pode acessar e usar variáveis e gerenciadores de conexões do pacote que os contém através de acessadores de tipo mais acentuado nas classes base geradas automaticamente. Contudo, você deve configurar as variáveis e os gerenciadores de conexões antes de digitar o modo de design de código, se quiser disponibilizá-los para seu script. Você também pode gerar eventos e executar log do código do componente Script.  
  
 Os itens de projeto gerados automaticamente no projeto do componente Script fornecem os seguintes objetos, métodos e propriedades para interagir com o pacote.  
  
|Recurso do Pacote|Método de Acesso|  
|---------------------|-------------------|  
|variáveis|Use as propriedades nomeadas e digitadas do acessador na classe de coleção **Variables** no item de projeto **ComponentWrapper**, expostas através da propriedade **Variables** da classe **ScriptMain**.<br /><br /> O método **PreExecute** só pode acessar variáveis somente leitura. O método **PostExecute** pode acessar variáveis somente leitura e de leitura/gravação.|  
|conexões|Use as propriedades nomeadas e digitadas do acessador na classe de coleção **Connections** no item de projeto **ComponentWrapper**, expostas através da propriedade **Connections** da classe **ScriptMain**.|  
|Eventos|Gere eventos usando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> da classe **ScriptMain** e os métodos **Fire\<X>** da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.|  
|Registro em log|Execute o registro em log usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> da classe **ScriptMain**.|  
  
## <a name="debugging-the-script-component"></a>Depurando o componente Script  
 Para depurar o código no seu componente Script, defina pelo menos um ponto de interrupção no código e, depois, feche o VSTA IDE para executar o pacote no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Quando a execução do pacote insere o componente Script, o VSTA IDE é reaberto e exibe seu código em modo somente leitura. Depois que a execução atingir seu ponto de interrupção, você poderá examinar valores de variáveis e passar pelo código restante.  
  
> [!NOTE]  
>  Você não pode depurar um componente Script quando executa-o como parte de um pacote filho que é executado a partir de uma tarefa Executar Pacote. Nessas circunstâncias, os pontos de interrupção definidos no componente Script no pacote filho são desconsiderados. Você pode depurar o pacote filho normalmente, executando-o separadamente.  
  
> [!NOTE]  
>  Quando você depura um pacote que contém vários componentes Script, o depurador depura um componente Script. O sistema poderá depurar outro componente Script se o depurador for concluído, como no caso de um contêiner Loop Foreach ou Loop For.  
  
 Você também pode monitorar a execução do componente Script usando os métodos seguintes:  
  
-   Interrompa a execução e exiba uma mensagem modal usando o método **MessageBox.Show** no namespace **System.Windows.Forms**. (Remova esse código após concluir o processo de depuração).  
  
-   Gere eventos para mensagens informativas, advertências e erros. Os métodos FireInformation, FireWarning e FireError exibem a descrição do evento na janela de **Saída** do Visual Studio. No entanto, o método FireProgress, o método Console.Write e o método Console.WriteLine não exibem nenhuma informação na janela de **Saída**. Mensagens do evento FireProgress aparecem na guia **Progresso** do Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obter mais informações, consulte [Acionando eventos no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md).  
  
-   Eventos de log ou mensagens definidas pelo usuário para provedores de log habilitados. Para obter mais informações, consulte [Registro em log no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md).  
  
 Caso queira apenas examinar a saída de um componente Script configurado como uma origem ou uma transformação, sem salvar os dados em um destino, você pode parar o fluxo de dados com uma [Transformação de Contagem de Linhas](../../../integration-services/data-flow/transformations/row-count-transformation.md) e anexar um visualizador de dados à saída do componente Script. Para obter informações sobre visualizadores de dados, consulte [Depurar o fluxo de dados](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Para obter mais informações sobre como codificar o componente Script, consulte os tópicos seguintes nesta seção.  
  
 [Compreender o Component Object Model do Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Explica como usar os objetos, métodos e propriedades disponíveis no componente Script.  
  
 [Referenciar outros assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Explica como referenciar objetos da biblioteca de classes [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] no componente Script.  
  
 [Simulando uma saída de erro para o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Explica como simular uma saída de erro para linhas que geram erros durante o processamento pelo componente Script.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [Problemas de instalação e configuração de VSTA nas instalações de SSIS 2008 e R2](https://docs.microsoft.com/archive/blogs/jason_howell/vsta-setup-and-configuration-troubles-for-ssis-2008-and-r2-installations), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o componente de Script no Editor de Componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  
