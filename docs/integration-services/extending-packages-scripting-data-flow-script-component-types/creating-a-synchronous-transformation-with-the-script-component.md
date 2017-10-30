---
title: "Criando uma transformação síncrona com o componente Script | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>Criando uma transformação síncrona com o componente Script
  Você usa um componente de transformação no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar e analisar dados à medida que eles passam da origem ao destino. Uma transformação com saídas síncronas processa cada linha de entrada que passa pelo componente. Uma transformação com saídas assíncronas espera até receber todas as linhas de entrada para completar seu processamento. Este tópico discute uma transformação síncrona. Para obter informações sobre transformações assíncronas, consulte [criando uma transformação assíncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md). Para obter mais informações sobre a diferença entre componentes síncronos e assíncronos, consulte [Noções básicas sobre síncrona e transformações assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obter uma visão geral do componente Script, consulte [estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas que devem ser seguidas no desenvolvimento de um componente de fluxo de dados personalizado na seção em [desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)e especialmente [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>Guia de Introdução com um componente de transformação síncrono  
 Quando você adiciona um componente Script ao painel fluxo de dados do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, o **Selecionar tipo de componente de Script** caixa de diálogo é aberta e solicita que você selecione um tipo de componente de origem, destino ou transformação. Na caixa de diálogo, selecione **transformação**.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>Configurando um componente de transformação síncrono em modo de design de metadados  
 Depois de selecionar a opção para criar um componente de transformação, configure o componente usando o **Editor de transformação scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para definir a linguagem de script para o componente Script, você deve definir o **ScriptLanguage** propriedade o **Script** página do **Editor de transformação scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem padrão de script para o componente Script, use o **linguagem de script** opção o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [erais página](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Um componente de transformação de fluxo de dados tem uma entrada e dá suporte a uma ou mais saídas. Configurando a entrada e as saídas do componente é uma das etapas que você deve concluir no modo de design de metadados, usando o **Editor de transformação scripts**, antes de escrever seu script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurando colunas de entrada  
 Um componente de transformação tem uma entrada.  
  
 No **colunas de entrada** página do **Editor de transformação de Script,** a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas que você deseja transformar ou percorrer. Marque qualquer coluna que você queira transformar no local como De leitura/gravação.  
  
 Para obter mais informações sobre o **colunas de entrada** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; página colunas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurando entradas, saídas e colunas de saída  
 Um componente de transformação dá suporte a uma ou mais saídas.  
  
 No **entradas e saídas** página do **Editor de transformação scripts**, você pode ver que uma única saída foi criada, mas a saída não tem colunas. Nessa página do editor, você pode precisar ou querer configurar os itens a seguir.  
  
-   Crie uma ou mais saídas adicionais, como uma saída de erro simulada para linhas que contêm valores inesperados. Use o **adicionar saída** e **remover saída** botões para gerenciar as saídas do seu componente de transformação síncrono. Todas as linhas de entrada são direcionadas para todas as saídas disponíveis, a menos que você indique que pretende redirecionar cada linha para uma ou outra saída. Indique que pretende redirecionar linhas especificando um valor inteiro diferente de zero para o **ExclusionGroup** propriedade nas saídas. O valor de inteiro específico inserido em **ExclusionGroup** identificar as saídas não é significativa, mas você deve usar o mesmo inteiro consistentemente para o grupo especificado de saídas.  
  
    > [!NOTE]  
    >  Você também pode usar uma diferente de zero **ExclusionGroup** valor da propriedade com uma única saída quando você não deseja que todas as linhas de saída. No entanto, nesse caso, você deve chamar explicitamente o **DirectRowTo\<outputbuffer >** método para cada linha que você deseja enviar para a saída.  
  
-   Atribua um nome mais descritivo para a entrada e as saídas. O componente Script utiliza esses nomes para gerar as propriedades de acessador digitadas que você utilizará para referenciar a entrada e as saídas no seu script.  
  
-   Deixe as colunas como estão nas transformações síncronas. Normalmente, uma transformação síncrona não acrescenta colunas ao fluxo de dados. Os dados são modificados no local no buffer, e o buffer é passado para o próximo componente do fluxo de dados. Se esse for o caso, você não terá que adicionar e configurar colunas de saída explicitamente nas saídas da transformação. As saídas aparecem no editor sem qualquer coluna explicitamente definida.  
  
-   Acrescente colunas novas a saídas de erro simuladas para erros em nível de linha. Normalmente a várias saídas no mesmo **ExclusionGroup** têm o mesmo conjunto de colunas de saída. Porém, se você estiver criando uma saída de erro simulada, pode ser que queira adicionar mais colunas para conter informações de erro. Para obter informações sobre como o mecanismo de fluxo de dados processa linhas de erro, consulte [usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). Observe que no componente Script você deve escrever seu próprio código para preencher as colunas adicionais com informações de erro apropriadas. Para obter mais informações, consulte [simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre o **entradas e saídas** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; entradas e saídas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se você quiser usar variáveis existentes em seu script, você pode adicioná-las a **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade o **Script** página das **Editor de transformação scripts**.  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Você também pode selecionar diversas variáveis clicando no botão de reticências (**...** ) ao lado de **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade e, em seguida, selecione as variáveis no **selecionar variáveis** caixa de diálogo.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre o **Script** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Script de página &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>Gerando scripts de um componente de transformação síncrono em modo de design de código  
 Depois de configurar os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de transformação scripts**, no **Script** , clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE onde você pode adicionar seu script personalizado. A linguagem de script que você usa depende se você selecionou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# como a linguagem de script para o **ScriptLanguage** propriedade o **Script** página.  
  
 Para obter informações importantes que se aplica a todos os tipos de componentes criados usando o componente Script, consulte [codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o VSTA IDE depois de criar e configurar um componente de transformação, o editável **ScriptMain** classe aparece no editor de códigos com um stub para o **ProcessInputRow** método. O **ScriptMain** classe é onde você escreverá seu código personalizado, e **ProcessInputRow** é o método mais importante em um componente de transformação.  
  
 Se você abrir o **Explorador de projeto** janela no VSTA, você pode ver que o componente Script também gerou somente leitura **BufferWrapper** e **ComponentWrapper** projeto itens. O **ScriptMain** classe herda o **UserComponent** classe no **ComponentWrapper** item de projeto.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o **ProcessInput** método no **UserComponent** de classe que substitui o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> classe pai. O **ProcessInput** método por sua vez percorre as linhas no buffer de entrada e chama o **ProcessInputRow** método uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Um componente de transformação com saídas síncronas é o mais simples de todos os componentes de fluxo de dados para gravar. Por exemplo, o exemplo de saída única mostrado mais adiante neste tópico consiste no seguinte código personalizado:  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 Para concluir a criação de um componente de transformação síncrono personalizado, você usa substituído **ProcessInputRow** método para transformar os dados em cada linha do buffer de entrada. O mecanismo de fluxo de dados transmite esse buffer, quando cheio, para o próximo componente do fluxo de dados.  
  
 Dependendo dos requisitos, você talvez queira gravar o script no **PreExecute** e **PostExecute** métodos, disponíveis no **ScriptMain** classe para executar processamento preliminar ou final.  
  
### <a name="working-with-multiple-outputs"></a>Trabalhando com várias saídas  
 Direcionar linhas de entrada a uma de duas ou mais saídas possíveis não requer muito mais código personalizado do que o cenário de saída única discutido anteriormente. Por exemplo, o exemplo de duas saídas mostrado mais adiante neste tópico consiste no seguinte código personalizado:  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 Neste exemplo, o componente Script gera o **DirectRowTo\<OutputBufferX >** métodos para você, com base nos nomes das saídas que você configurou. Você pode usar um código semelhante para direcionar linhas de erro a uma saída de erro simulada.  
  
## <a name="examples"></a>Exemplos  
 Estes exemplos demonstram o código personalizado que é necessário o **ScriptMain** classe para criar um componente de transformação síncrono.  
  
> [!NOTE]  
>  Esses exemplos usam o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo e passam a primeira e a quarta colunas, o **intAddressID** e  **Cidade nvarchar (30)** colunas, por meio do fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="single-output-synchronous-transformation-example"></a>Exemplo de transformação síncrona de saída única  
 Este exemplo demonstra um componente de transformação síncrono com uma única saída. Essa transformação passa o **AddressID** coluna e converte o **Cidade** coluna em maiusculas.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de uma outra transformação ao novo componente de transformação no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Essa saída deve fornecer dados do **Person. address** analítico o **AdventureWorks** banco de dados de exemplo que contém o **AddressID** e **cidade**  colunas.  
  
3.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas. Marca o **City** coluna como leitura/gravação.  
  
4.  Sobre o **entradas e saídas** página, renomeie a entrada e saída com nomes mais descritivos, como **MyAddressInput** e **MyAddressOutput**. Observe que o **SynchronousInputID** da saída corresponde a **ID** da entrada. Portanto, não é necessário adicionar e configurar colunas de saída.  
  
5.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de transformação scripts**.  
  
6.  Criar e configurar um componente de destino que espera o **AddressID** e **City** colunas, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Então, conecte a saída da transformação ao componente de destino. Você pode criar uma tabela de destino executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] do **AdventureWorks** banco de dados:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Execute o exemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>Exemplo de transformação síncrona com duas saídas  
 Este exemplo demonstra um componente de transformação síncrono com duas saídas. Essa transformação passa o **AddressID** coluna e converte o **Cidade** coluna em maiusculas. Se o nome de cidade for Redmond, ele direcionará a linha para uma saída e todas as outras linhas para outra saída.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de uma outra transformação ao novo componente de transformação no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Essa saída deve fornecer dados a partir de **Person. address** tabela do **AdventureWorks** banco de dados de exemplo que contém pelo menos o **AddressID** e  **Cidade** colunas.  
  
3.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas. Marca o **City** coluna como leitura/gravação.  
  
4.  Sobre o **entradas e saídas** página, crie uma segunda saída. Depois de adicionar a nova saída, certifique-se de que você defina sua **SynchronousInputID** para o **ID** da entrada. Essa propriedade já está definida na primeira saída, que é criada por padrão. Para cada saída, defina o **ExclusionGroup** propriedade com o mesmo valor diferente de zero para indicar que você dividirá as linhas de entrada entre duas saídas mutuamente exclusivas. Não é necessário acrescentar qualquer coluna de saída às saídas.  
  
5.  Renomeie a entrada e as saídas com nomes mais descritivos, como **MyAddressInput**, **MyRedmondAddresses**, e **MyOtherAddresses**.  
  
6.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de transformação scripts**.  
  
7.  Criar e configurar os dois componentes de destino que esperam o **AddressID** e **City** colunas, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, um destino de arquivo simples ou o componente de destino de exemplo demonstrada [criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Em seguida, conecte cada uma das saídas da transformação a um dos componentes de destino. Você pode criar tabelas de destino executando um [!INCLUDE[tsql](../../includes/tsql-md.md)] comando semelhante ao seguinte (com nomes de tabela exclusivo) no **AdventureWorks** banco de dados:  
  
    ```sql
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  Execute o exemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transformações síncronas e assíncronas] (~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [Criação de uma transformação assíncrona com o componente Script] (~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [Desenvolvendo um componente de transformação personalizado com saídas síncronas] (~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



