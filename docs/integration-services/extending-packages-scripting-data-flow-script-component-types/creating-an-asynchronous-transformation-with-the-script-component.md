---
title: "Criando uma transformação assíncrona com o componente Script | Microsoft Docs"
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Criando uma transformação assíncrona com o componente Script
  Você usa um componente de transformação no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar e analisar dados à medida que eles passam da origem ao destino. Uma transformação com saídas síncronas processa cada linha de entrada que passa pelo componente. Uma transformação com saídas assíncronas pode aguardar para concluir seu processamento até que a transformação recebeu todas as linhas de entrada ou a transformação pode gerar algumas linhas antes de receber todas as linhas de entrada. Esse tópico discute uma transformação assíncrona. Se o processamento exigir uma transformação síncrona, consulte [criando uma transformação síncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Para obter mais informações sobre as diferenças entre componentes síncronos e assíncronos, consulte [Noções básicas sobre síncrona e transformações assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obter uma visão geral do componente Script, consulte [estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas que devem ser seguidas no desenvolvimento de um componente de fluxo de dados personalizados no [desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) seção, e especialmente [desenvolvendo um componente de transformação personalizado com saídas síncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Guia de Introdução com um componente de transformação assíncrono  
 Quando você adiciona um componente Script à guia fluxo de dados de [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, o **Selecionar tipo de componente de Script** caixa de diálogo é exibida, solicitando que você pré-configure o componente como uma origem, transformação ou destino. Na caixa de diálogo, selecione **transformação**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Configurando um componente de transformação assíncrono em modo do design de metadados  
 Depois de selecionar a opção para criar um componente de transformação, configure o componente usando o **Editor de transformação scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para selecionar a linguagem de script que o componente Script utilizará, defina o **ScriptLanguage** propriedade o **Script** página do **Editor de transformação scripts** caixa de diálogo caixa.  
  
> [!NOTE]  
>  Para definir a linguagem padrão de script para o componente Script, use o **linguagem de script** opção o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Um componente de transformação de fluxo de dados tem uma entrada e dá suporte a uma ou mais saídas. Configuração de entrada e saídas de seu componente é uma das etapas que você deve concluir no modo de design de metadados, usando o **Editor de transformação scripts**, antes de escrever seu script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurando colunas de entrada  
 Um componente de transformação criado através do componente Script tem uma única entrada.  
  
 Sobre o **colunas de entrada** página do **Editor de transformação scripts**, a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas que você deseja transformar ou percorrer. Marque qualquer coluna que você queira transformar no local como De leitura/gravação.  
  
 Para obter mais informações sobre o **colunas de entrada** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; página colunas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurando entradas, saídas e colunas de saída  
 Um componente de transformação dá suporte a uma ou mais saídas.  
  
 Frequentemente, uma transformação com saídas assíncronas possui duas saídas. Por exemplo, ao contar o número de endereços localizados em uma cidade específica, talvez você queira transmitir os dados do endereço para uma saída, enquanto envia o resultado da agregação para outra saída. A saída de agregação também exige uma coluna de saída nova.  
  
 No **entradas e saídas** página do **Editor de transformação scripts**, você vê que uma única saída foi criada por padrão, mas nenhuma coluna de saída foi criada. Nessa página do editor, você pode configurar os seguintes itens:  
  
-   Talvez você queira criar uma ou mais saídas adicionais, como uma saída para o resultado de uma agregação. Use o **adicionar saída** e **remover saída** botões para gerenciar as saídas do seu componente de transformação assíncrono. Definir o **SynchronousInputID** propriedade de cada saída como zero para indicar que a saída não simplesmente passando dados de um componente upstream ou transformá-los em lugar de linhas e colunas existentes. É essa configuração que torna as saídas assíncronas para a entrada.  
  
-   Talvez você queira atribuir um nome amigável à entrada e saídas. O componente Script utiliza esses nomes para gerar as propriedades de acessador digitadas que você utilizará para referenciar a entrada e as saídas no seu script.  
  
-   Frequentemente, uma transformação assíncrona adiciona colunas ao fluxo de dados. Quando o **SynchronousInputID** de uma saída é zero, indicando que a saída não simplesmente passando dados de um componente upstream ou transformá-los em lugar de linhas e colunas existentes, você deve adicionar e configurar colunas de saída explicitamente na saída. Colunas de saída não precisam ter os mesmos nomes que as colunas de entrada para as quais elas são mapeadas.  
  
-   Talvez você queira adicionar mais colunas para incluir informações adicionais. Escreva seu próprio código para preencher as colunas adicionais com dados. Para obter informações sobre como reproduzir o comportamento de uma saída de erro padrão, consulte [simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre o **entradas e saídas** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; entradas e saídas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se houver qualquer variáveis cujos valores você deseja usar em seu script, você pode adicioná-los nos campos de propriedade ReadOnlyVariables e ReadWriteVariables no **Script** página de **Editor de transformação scripts** .  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Você também pode selecionar diversas variáveis clicando no botão de reticências (**...** ) ao lado de **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade e, em seguida, selecione as variáveis no **selecionar variáveis** caixa de diálogo.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre o **Script** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Script de página &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Gerando scripts de um componente de transformação assíncrono em modo do design de código  
 Depois de configurar todos os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de transformação scripts**, no **Script** , clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE onde você pode adicionar seu script personalizado. A linguagem de script que você usa depende se você selecionou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# como a linguagem de script para o **ScriptLanguage** propriedade o **Script** página.  
  
 Para obter informações importantes que se aplica a todos os tipos de componentes criados usando o componente Script, consulte [codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o VSTA IDE depois de criar e configurar um componente de transformação, o editável **ScriptMain** classe aparece no editor de códigos com stubs para o ProcessInputRow e os métodos de CreateNewOutputRows. A classe ScriptMain é onde você escreverá seu código personalizado e ProcessInputRow é o método mais importante em um componente de transformação. O **CreateNewOutputRows** método é geralmente mais usado em um componente de origem, que é como uma transformação assíncrona em que ambos os componentes devem criar suas próprias linhas de saída.  
  
 Se você abrir o VSTA **Explorador de projeto** janela, você pode ver que o componente Script também gerou somente leitura **BufferWrapper** e **ComponentWrapper** itens de projeto . A classe de ScriptMain herda da classe UserComponent o **ComponentWrapper** item de projeto.  
  
 Em tempo de execução, o mecanismo de fluxo de dados chama o método PrimeOutput **UserComponent** de classe que substitui o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> método o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> classe pai. O método PrimeOutput por sua vez chama o método CreateNewOutputRows.  
  
 Em seguida, o mecanismo de fluxo de dados invoca o método ProcessInput na classe UserComponent, que substitui o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> classe pai. Por sua vez, o método ProcessInput percorre as linhas no buffer de entrada e chama o método ProcessInputRow uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para concluir a criação de um componente de transformação assíncrono personalizado, você deve usar o método ProcessInputRow substituído para processar os dados em cada linha do buffer de entrada. Como as saídas não são síncronas para a entrada, escreva explicitamente linhas de dados para as saídas.  
  
 Em uma transformação assíncrona, você pode usar o método AddRow para adicionar linhas à saída, conforme apropriado dentro dos métodos ProcessInputRow ou ProcessInput. Você não precisa usar o método CreateNewOutputRows. Se você estiver escrevendo uma única linha de resultados, como os de agregação a uma saída específica, você pode criar a linha de saída com antecedência usando o método CreateNewOutputRows e preencher seus valores posteriormente após o processamento de todas as linhas de entrada. No entanto não é útil criar várias linhas no método CreateNewOutputRows, porque o componente Script só permite que você use a linha atual em uma entrada ou saída. O método CreateNewOutputRows é mais importante em um componente de origem em que não há nenhuma linha de entrada para processar.  
  
 Você talvez queira substituir o método ProcessInput em si, para que você possa fazer preliminar ou final de processamento adicional antes ou depois que você percorra o buffer de entrada e chamar ProcessInputRow para cada linha. Por exemplo, um dos exemplos de código neste tópico substitui ProcessInput para contar o número de endereços de uma cidade específica como ProcessInputRow executa um loop em linhas**.** O exemplo grava o valor de resumo para a segunda saída depois que todas as linhas forem processadas. O exemplo completa a saída em ProcessInput porque os buffers de saída não estão mais disponíveis quando PostExecute é chamado.  
  
 Dependendo dos requisitos, você talvez queira gravar o script nos métodos PreExecute e PostExecute disponíveis na classe ScriptMain para executar qualquer processamento preliminar ou final.  
  
> [!NOTE]  
>  Se você estivesse desenvolvendo um componente de fluxo de dados personalizados do zero, seria importante substituir o método PrimeOutput para referências de cache aos buffers de saída para que você pode adicionar linhas de dados aos buffers de mais tarde. No componente Script, isso não é necessário porque você tem uma classe gerada automaticamente que representa cada buffer de saída no **BufferWrapper** item de projeto.  
  
## <a name="example"></a>Exemplo  
 Este exemplo demonstra o código personalizado que é necessário na classe ScriptMain para criar um componente de transformação assíncrono.  
  
> [!NOTE]  
>  Esses exemplos usam o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo e passam a primeira e a quarta colunas, o **intAddressID** e  **Cidade nvarchar (30)** colunas, por meio do fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
 Esse exemplo demonstra um componente de transformação assíncrono com duas saídas. Essa transformação passa o **AddressID** e **City** colunas para uma saída, enquanto ele conta o número de endereços localizados em uma cidade específica (Redmond, Washington, Estados Unidos) e, em seguida, as saídas de valor resultante para uma segunda saída.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de outra transformação para o novo componente de transformação no designer. Essa saída deve fornecer dados a partir de **Person. address** tabela do **AdventureWorks** banco de dados de exemplo que contém pelo menos o **AddressID** e  **Cidade** colunas.  
  
3.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas.  
  
4.  Sobre o **entradas e saídas** página, adicione e configure o **AddressID** e **Cidade** colunas na primeira saída de saída. Adicione uma segunda saída e uma coluna de saída para obter o valor resumido na segunda saída. Defina a propriedade SynchronousInputID da primeira saída como 0, pois esse exemplo copia cada linha de entrada explicitamente na primeira saída. A propriedade SynchronousInputID da saída recém-criada já está definida como 0.  
  
5.  Renomeie a entrada, as saídas e a nova coluna de saída para atribuir a elas nomes mais descritivos. O exemplo usa **MyAddressInput** como o nome da entrada, **MyAddressOutput** e **MySummaryOutput** para as saídas, e **MyRedmondCount** para a coluna de saída na segunda saída.  
  
6.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de transformação scripts**.  
  
7.  Criar e configurar um componente de destino para a primeira saída que espera o **AddressID** e **City** colunas, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino ou o componente de destino de exemplo demonstrada [criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md),. Em seguida, conecte-se a primeira saída da transformação, **MyAddressOutput**, para o componente de destino. Você pode criar uma tabela de destino executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] do **AdventureWorks** banco de dados:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Crie e configure outro componente de destino para a segunda saída. Em seguida, conecte-se a segunda saída da transformação, **MySummaryOutput**, para o componente de destino. Como a segunda saída grava uma única linha com um único valor, você pode facilmente configurar um destino com um gerenciador de conexões de arquivo simples que se conecta a um novo arquivo que possui uma única coluna. No exemplo, essa coluna de destino é nomeada **MyRedmondCount**.  
  
9. Execute o exemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transformações síncronas e assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Criando uma transformação síncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

