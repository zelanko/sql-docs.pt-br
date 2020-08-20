---
description: Criando uma transformação assíncrona com o componente Script
title: Criando uma transformação assíncrona com o componente Script | Microsoft Docs
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 05d28638ebb8981c0ccce4e6bb38ab7179565d00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495603"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Criando uma transformação assíncrona com o componente Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Você usa um componente de transformação no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar e analisar dados à medida que eles passam da origem ao destino. Uma transformação com saídas síncronas processa cada linha de entrada que passa pelo componente. Uma transformação com saídas assíncronas pode aguardar para concluir seu processamento depois de receber todas as linhas de entrada ou ela pode gerar algumas linhas antes de receber todas as linhas de entrada. Esse tópico discute uma transformação assíncrona. Se o processamento exigir uma transformação síncrona, consulte [Criando uma transformação síncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Para obter mais informações sobre as diferenças entre componentes síncronos e assíncronos, consulte [Compreendendo as transformações síncronas e assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obter uma visão geral do componente Script, consulte [Estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas que devem ser seguidas no desenvolvimento de um componente de fluxo de dados personalizado na seção de [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e, especialmente, [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Guia de Introdução com um componente de transformação assíncrono  
 Quando você adiciona um componente Script à guia Fluxo de Dados do Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], a caixa de diálogo **Selecionar Tipo de Componente Script** é exibida, solicitando a pré-configuração do componente como uma origem, uma transformação ou um destino. Nessa caixa de diálogo, selecione **Transformação**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Configurando um componente de transformação assíncrono em modo do design de metadados  
 Depois de selecionar a opção para criar um componente de transformação, configure o componente usando o **Editor de Transformação Scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de Componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para selecionar a linguagem de script que será usada pelo componente Script, defina a propriedade **ScriptLanguage** na página **Script** da caixa de diálogo **Editor de Transformação Scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem de scripts padrão para o componente Script, use a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](../general-page-of-integration-services-designers-options.md).  
  
 Um componente de transformação de fluxo de dados tem uma entrada e dá suporte a uma ou mais saídas. A configuração da entrada e das saídas do componente é uma das etapas que devem ser concluídas no modo de design de metadados, usando o **Editor de Transformação Scripts**, antes de escrever o script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurando colunas de entrada  
 Um componente de transformação criado através do componente Script tem uma única entrada.  
  
 Na página **Colunas de Entrada** do **Editor de Transformação Scripts**, a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas que você deseja transformar ou percorrer. Marque qualquer coluna que você queira transformar no local como De leitura/gravação.  
  
 Para obter mais informações sobre a página **Colunas de Entrada** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Colunas de Entrada&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurando entradas, saídas e colunas de saída  
 Um componente de transformação dá suporte a uma ou mais saídas.  
  
 Frequentemente, uma transformação com saídas assíncronas possui duas saídas. Por exemplo, ao contar o número de endereços localizados em uma cidade específica, talvez você queira transmitir os dados do endereço para uma saída, enquanto envia o resultado da agregação para outra saída. A saída de agregação também exige uma coluna de saída nova.  
  
 Na página **Entradas e Saídas** de **Editor de Transformação Scripts**, você verá que uma única saída foi criada por padrão, mas que nenhuma coluna de saída foi criada. Nessa página do editor, você pode configurar os seguintes itens:  
  
-   Talvez você queira criar uma ou mais saídas adicionais, como uma saída para o resultado de uma agregação. Use os botões **Adicionar Saída** e **Remover Saída** para gerenciar as saídas do componente de transformação assíncrona. Defina a propriedade **SynchronousInputID** de cada saída como zero para indicar que a saída não está simplesmente passando dados de um componente upstream nem transformando-os in-loco nas linhas e colunas existentes. É essa configuração que torna as saídas assíncronas para a entrada.  
  
-   Talvez você queira atribuir um nome amigável à entrada e saídas. O componente Script utiliza esses nomes para gerar as propriedades de acessador digitadas que você utilizará para referenciar a entrada e as saídas no seu script.  
  
-   Frequentemente, uma transformação assíncrona adiciona colunas ao fluxo de dados. Quando a propriedade **SynchronousInputID** de uma saída for zero, indicando que a saída não está simplesmente passando dados de um componente upstream nem transformando-os in-loco nas linhas e colunas existentes, adicione e configure colunas de saída de maneira explícita na saída. Colunas de saída não precisam ter os mesmos nomes que as colunas de entrada para as quais elas são mapeadas.  
  
-   Talvez você queira adicionar mais colunas para incluir informações adicionais. Escreva seu próprio código para preencher as colunas adicionais com dados. Para obter informações sobre como reproduzir o comportamento de uma saída de erro padrão, consulte [Simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre a página **Entradas e Saídas** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Entradas e Saídas&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Caso existam variáveis cujos valores você deseja usar no script, adicione-as aos campos de propriedade ReadOnlyVariables e ReadWriteVariables da página **Script** do **Editor de Transformação Scripts**.  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Outra alternativa é selecionar diversas variáveis clicando no botão de reticências ( **...** ) ao lado dos campos de propriedade **ReadOnlyVariables** e **ReadWriteVariables** e, em seguida, selecionar as variáveis na caixa de diálogo **Selecionar variáveis**.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [Usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Script** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Script&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Gerando scripts de um componente de transformação assíncrono em modo do design de código  
 Depois de configurar todos os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de Transformação Scripts**, na página **Script**, clique em **Editar Script** para abrir o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications), no qual você pode adicionar o script personalizado. A linguagem de scripts usada depende se você selecionou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como a linguagem de scripts para a propriedade **ScriptLanguage** na página **Script**.  
  
 Para obter informações importantes que se aplicam a todos os tipos de componentes criados por meio do componente Script, consulte [Codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o IDE do VSTA depois de criar e configurar um componente de transformação, a classe editável **ScriptMain** é exibida no editor de códigos com stubs para os métodos ProcessInputRow e CreateNewOutputRows. A classe ScriptMain é o local em que você escreverá seu código personalizado e ProcessInputRow é o método mais importante em um componente de transformação. O método **CreateNewOutputRows** costuma ser mais usado em um componente de origem, que é como uma transformação assíncrona, pois ambos os componentes devem criar suas próprias linhas de saída.  
  
 Se você abrir a janela **Explorador de Projeto** do VSTA, verá que o componente Script também gerou os itens de projeto **BufferWrapper** e **ComponentWrapper** somente leitura. A classe ScriptMain herda da classe UserComponent no item de projeto **ComponentWrapper**.  
  
 Em tempo de execução, o mecanismo de fluxo de dados chama o método PrimeOutput na classe **UserComponent**, que substitui o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O método PrimeOutput, por sua vez, chama o método CreateNewOutputRows.  
  
 Depois, o mecanismo de fluxo de dados invoca o método ProcessInput na classe UserComponent, que substitui o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O método ProcessInput, por sua vez, executa um loop nas linhas do buffer de entrada e chama o método ProcessInputRow uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para concluir a criação de um componente de transformação assíncrona personalizado, use o método ProcessInputRow substituído para processar os dados em cada linha do buffer de entrada. Como as saídas não são síncronas para a entrada, escreva explicitamente linhas de dados para as saídas.  
  
 Em uma transformação assíncrona, você pode usar o método AddRow para adicionar linhas à saída, conforme apropriado, dentro do método ProcessInputRow ou ProcessInput. Você não precisa usar o método CreateNewOutputRows. Se estiver escrevendo uma única linha de resultados, como resultados de agregação, para determinada saída, crie a linha de saída antecipadamente usando o método CreateNewOutputRows e preencha seus valores posteriormente, depois de processar todas as linhas de entrada. Contudo, não é útil criar múltiplas linhas no método CreateNewOutputRows, pois o componente Script só permite o uso da linha atual em uma entrada ou saída. O método CreateNewOutputRows é mais importante em um componente de origem em que não há linhas de entrada a serem processadas.  
  
 É recomendável substituir o próprio método ProcessInput. Isso permite executar um processamento preliminar ou final adicional antes ou depois de executar um loop no buffer de entrada e chamar ProcessInputRow para cada linha. Por exemplo, um dos exemplos de código deste tópico substitui ProcessInput para contar o número de endereços em uma cidade específica, conforme ProcessInputRow executa um loop pelas linhas **.** O exemplo grava o valor de resumo na segunda saída depois que todas as linhas foram processadas. O exemplo completa a saída em ProcessInput porque os buffers de saída não estão mais disponíveis quando PostExecute é chamado.  
  
 Dependendo dos requisitos, é recomendável escrever o script nos métodos PreExecute e PostExecute disponíveis na classe ScriptMain para executar qualquer processamento preliminar ou final.  
  
> [!NOTE]  
>  Se estiver desenvolvendo um componente de fluxo de dados personalizado a partir do zero, será importante substituir o método PrimeOutput para referências de cache aos buffers de saída, de modo que você possa adicionar linhas de dados aos buffers posteriormente. No componente Script, isso não é necessário porque você tem uma classe gerada automaticamente que representa cada buffer de saída no item de projeto **BufferWrapper**.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo demonstra o código personalizado que é necessário na classe ScriptMain para criar um componente de transformação assíncrona.  
  
> [!NOTE]  
>  Esses exemplos usam a tabela **Person.Address** no banco de dados de exemplo **AdventureWorks** e passam sua primeira e quarta colunas, as colunas **intAddressID** e **nvarchar(30)City**, pelo fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
 Esse exemplo demonstra um componente de transformação assíncrono com duas saídas. Essa transformação passa pelas colunas **AddressID** e **City** para uma saída, enquanto conta o número de endereços localizados em uma cidade específica (Redmond, Washington, EUA) e, depois, gera o valor resultante para uma segunda saída.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de outra transformação para o novo componente de transformação no designer. Essa saída deve fornecer dados da tabela **Person.Address** do banco de dados de exemplo **AdventureWorks** que contêm, pelo menos, as colunas **AddressID** e **City**.  
  
3.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas **AddressID** e **City**.  
  
4.  Na página **Entradas e Saídas**, adicione e configure as colunas de saída **AddressID** e **City** na primeira saída. Adicione uma segunda saída e uma coluna de saída para obter o valor resumido na segunda saída. Defina a propriedade SynchronousInputID da primeira saída como 0, pois esse exemplo copia cada linha de entrada explicitamente na primeira saída. A propriedade SynchronousInputID da saída recém-criada já está definida como 0.  
  
5.  Renomeie a entrada, as saídas e a nova coluna de saída para atribuir a elas nomes mais descritivos. O exemplo usa **MyAddressInput** como o nome da entrada, **MyAddressOutput** e **MySummaryOutput** para as saídas e **MyRedmondCount** para a coluna de saída na segunda saída.  
  
6.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**.  
  
7.  Crie e configure um componente de destino para a primeira saída que espera as colunas **AddressID** e **City**, como um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Depois, conecte a primeira saída da transformação, **MyAddressOutput**, ao componente de destino. Crie uma tabela de destino executando o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Crie e configure outro componente de destino para a segunda saída. Depois, conecte a segunda saída da transformação, **MySummaryOutput**, ao componente de destino. Como a segunda saída grava uma única linha com um único valor, você pode facilmente configurar um destino com um gerenciador de conexões de arquivo simples que se conecta a um novo arquivo que possui uma única coluna. No exemplo, essa coluna de destino é chamada **MyRedmondCount**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Compreender as transformações síncronas e assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Criando uma transformação síncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
