---
title: Criando uma transformação síncrona com o componente Script | Microsoft Docs
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ae3d3988fbf21eb133e204e613dcaaf2401fda53
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112378"
---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>Criando uma transformação síncrona com o componente Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Você usa um componente de transformação no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar e analisar dados à medida que eles passam da origem ao destino. Uma transformação com saídas síncronas processa cada linha de entrada que passa pelo componente. Uma transformação com saídas assíncronas espera até receber todas as linhas de entrada para completar seu processamento. Este tópico discute uma transformação síncrona. Para obter informações sobre transformações assíncronas, consulte [Criando uma transformação assíncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md). Para obter mais informações sobre a diferença entre componentes síncronos e assíncronos, consulte [Compreender as transformações síncronas e assíncronas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obter uma visão geral do componente Script, consulte [Estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas que devem ser seguidas no desenvolvimento de um componente de fluxo de dados personalizado na seção de [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e, especialmente, [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>Guia de Introdução com um componente de transformação síncrono  
 Quando você adiciona um componente Script ao painel Fluxo de Dados do Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], a caixa de diálogo **Selecionar Tipo de Componente Script** é aberta e solicita a seleção de um tipo de componente de Origem, Destino ou Transformação. Nessa caixa de diálogo, selecione **Transformação**.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>Configurando um componente de transformação síncrono em modo de design de metadados  
 Depois de selecionar a opção para criar um componente de transformação, configure o componente usando o **Editor de Transformação Scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de Componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para definir a linguagem de script para o componente Script, defina a propriedade **ScriptLanguage** na página **Script** do **Editor de Transformação Scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem de scripts padrão para o componente Script, use a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [Página Geral](../general-page-of-integration-services-designers-options.md).  
  
 Um componente de transformação de fluxo de dados tem uma entrada e dá suporte a uma ou mais saídas. A configuração da entrada e das saídas do componente é uma das etapas que devem ser concluídas no modo de design de metadados, usando o **Editor de Transformação Scripts**, antes de escrever o script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurando colunas de entrada  
 Um componente de transformação tem uma entrada.  
  
 Na página **Colunas de Entrada** do **Editor de Transformação Scripts**, a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas que você deseja transformar ou percorrer. Marque qualquer coluna que você queira transformar no local como De leitura/gravação.  
  
 Para obter mais informações sobre a página **Colunas de Entrada** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Colunas de Entrada&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurando entradas, saídas e colunas de saída  
 Um componente de transformação dá suporte a uma ou mais saídas.  
  
 Na página **Entradas e Saídas** do **Editor de Transformação Scripts**, você poderá ver que uma única saída foi criada, mas que a saída não tem nenhuma coluna. Nessa página do editor, você pode precisar ou querer configurar os itens a seguir.  
  
-   Crie uma ou mais saídas adicionais, como uma saída de erro simulada para linhas que contêm valores inesperados. Use os botões **Adicionar Saída** e **Remover Saída** para gerenciar as saídas do componente de transformação síncrona. Todas as linhas de entrada são direcionadas para todas as saídas disponíveis, a menos que você indique que pretende redirecionar cada linha para uma ou outra saída. Você indica que pretende redirecionar linhas especificando um valor inteiro diferente de zero para a propriedade **ExclusionGroup** nas saídas. O valor inteiro específico inserido em **ExclusionGroup** para identificar as saídas não é significativo, mas você deve usar o mesmo inteiro de forma consistente para o grupo especificado de saídas.  
  
    > [!NOTE]  
    >  Também use um valor da propriedade **ExclusionGroup** diferente de zero com uma única saída quando não desejar gerar todas as linhas. No entanto, nesse caso, você deve chamar explicitamente o método **DirectRowTo\<outputbuffer>** para cada linha que deseja enviar à saída.  
  
-   Atribua um nome mais descritivo para a entrada e as saídas. O componente Script utiliza esses nomes para gerar as propriedades de acessador digitadas que você utilizará para referenciar a entrada e as saídas no seu script.  
  
-   Deixe as colunas como estão nas transformações síncronas. Normalmente, uma transformação síncrona não acrescenta colunas ao fluxo de dados. Os dados são modificados no local no buffer, e o buffer é passado para o próximo componente do fluxo de dados. Se esse for o caso, você não terá que adicionar e configurar colunas de saída explicitamente nas saídas da transformação. As saídas aparecem no editor sem qualquer coluna explicitamente definida.  
  
-   Acrescente colunas novas a saídas de erro simuladas para erros em nível de linha. De maneira geral, múltiplas saídas no mesmo **ExclusionGroup** têm o mesmo conjunto de colunas de saída. Porém, se você estiver criando uma saída de erro simulada, pode ser que queira adicionar mais colunas para conter informações de erro. Para obter informações sobre como o mecanismo de fluxo de dados processa linhas de erro, consulte [Usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). Observe que no componente Script você deve escrever seu próprio código para preencher as colunas adicionais com informações de erro apropriadas. Para obter mais informações, consulte [Simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre a página **Entradas e Saídas** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Entradas e Saídas&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se desejar usar variáveis existentes no script, adicione-as aos campos de propriedade **ReadOnlyVariables** e **ReadWriteVariables** na página **Script** do **Editor de Transformação Scripts**.  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Outra alternativa é selecionar diversas variáveis clicando no botão de reticências ( **...** ) ao lado dos campos de propriedade **ReadOnlyVariables** e **ReadWriteVariables** e, em seguida, selecionar as variáveis na caixa de diálogo **Selecionar variáveis**.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [Usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Script** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Script&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>Gerando scripts de um componente de transformação síncrono em modo de design de código  
 Depois de configurar os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de Transformação Scripts**, na página **Script**, clique em **Editar Script** para abrir o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications), no qual você pode adicionar o script personalizado. A linguagem de scripts usada depende se você selecionou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como a linguagem de scripts para a propriedade **ScriptLanguage** na página **Script**.  
  
 Para obter informações importantes que se aplicam a todos os tipos de componentes criados por meio do componente Script, consulte [Codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o IDE do VSTA depois de criar e configurar um componente de transformação, a classe editável **ScriptMain** é exibida no editor de códigos com um stub para o método **ProcessInputRow**. A classe **ScriptMain** é o local em que você escreverá seu código personalizado e **ProcessInputRow** é o método mais importante em um componente de transformação.  
  
 Se você abrir a janela **Explorador de Projeto** no VSTA, verá que o componente Script também gerou os itens de projeto **BufferWrapper** e **ComponentWrapper** somente leitura. A classe **ScriptMain** herda da classe **UserComponent** no item de projeto **ComponentWrapper**.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o método **ProcessInput** na classe **UserComponent**, que substitui o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O método **ProcessInput**, por sua vez, executa um loop nas linhas do buffer de entrada e chama o método **ProcessInputRow** uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Um componente de transformação com saídas síncronas é o mais simples de todos os componentes de fluxo de dados para gravar. Por exemplo, o exemplo de saída única mostrado mais adiante neste tópico consiste no seguinte código personalizado:  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 Para concluir a criação de um componente de transformação síncrona personalizado, use o método **ProcessInputRow** substituído para transformar os dados em cada linha do buffer de entrada. O mecanismo de fluxo de dados transmite esse buffer, quando cheio, para o próximo componente do fluxo de dados.  
  
 Dependendo dos requisitos, é recomendável escrever o script nos métodos **PreExecute** e **PostExecute** disponíveis na classe **ScriptMain** para executar um processamento preliminar ou final.  
  
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
  
 Neste exemplo, o componente Script gera os métodos **DirectRowTo\<OutputBufferX>** para você baseando-se nos nomes das saídas que foram configurados. Você pode usar um código semelhante para direcionar linhas de erro a uma saída de erro simulada.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos aqui demonstram o código personalizado que é necessário na classe **ScriptMain** para criar um componente de transformação síncrona.  
  
> [!NOTE]  
>  Esses exemplos usam a tabela **Person.Address** no banco de dados de exemplo **AdventureWorks** e passam sua primeira e quarta colunas, as colunas **intAddressID** e **nvarchar(30)City**, pelo fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="single-output-synchronous-transformation-example"></a>Exemplo de transformação síncrona de saída única  
 Este exemplo demonstra um componente de transformação síncrono com uma única saída. Essa transformação passa pela coluna **AddressID** e converte a coluna **City** em maiúsculas.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de uma outra transformação ao novo componente de transformação no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Essa saída deve fornecer dados da tabela **Person.Address** do banco de dados de exemplo **AdventureWorks**, que contém as colunas **AddressID** e **City**.  
  
3.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas **AddressID** e **City**. Marque a coluna **City** como Leitura/Gravação.  
  
4.  Na página **Entradas e Saídas**, renomeie a entrada e a saída com nomes mais descritivos, como **MyAddressInput** e **MyAddressOutput**. Observe que a **SynchronousInputID** da saída corresponde à **ID** da entrada. Portanto, não é necessário adicionar e configurar colunas de saída.  
  
5.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**.  
  
6.  Crie e configure um componente de destino que espera as colunas **AddressID** e **City**, como um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Então, conecte a saída da transformação ao componente de destino. Crie uma tabela de destino executando o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados **AdventureWorks**:  
  
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
 Este exemplo demonstra um componente de transformação síncrono com duas saídas. Essa transformação passa pela coluna **AddressID** e converte a coluna **City** em maiúsculas. Se o nome de cidade for Redmond, ele direcionará a linha para uma saída e todas as outras linhas para outra saída.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
2.  Conecte a saída de uma origem ou de uma outra transformação ao novo componente de transformação no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Essa saída deve fornecer dados da tabela **Person.Address** do banco de dados de exemplo **AdventureWorks** que contêm, pelo menos, as colunas **AddressID** e **City**.  
  
3.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas **AddressID** e **City**. Marque a coluna **City** como Leitura/Gravação.  
  
4.  Na página **Entradas e Saídas**, crie uma segunda saída. Depois de adicionar a nova saída, defina sua **SynchronousInputID** como a **ID** da entrada. Essa propriedade já está definida na primeira saída, que é criada por padrão. Para cada saída, defina a propriedade **ExclusionGroup** com o mesmo valor diferente de zero para indicar que você dividirá as linhas de entrada entre duas saídas mutuamente exclusivas. Não é necessário acrescentar qualquer coluna de saída às saídas.  
  
5.  Renomeie a entrada e as saídas com nomes mais descritivos, como **MyAddressInput**, **MyRedmondAddresses** e **MyOtherAddresses**.  
  
6.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**.  
  
7.  Crie e configure dois componentes de destino que esperam as colunas **AddressID** e **City**, como um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um destino de Arquivo Simples ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Em seguida, conecte cada uma das saídas da transformação a um dos componentes de destino. Crie tabelas de destino executando um comando [!INCLUDE[tsql](../../includes/tsql-md.md)] semelhante ao seguinte (com nomes de tabela exclusivos) no banco de dados **AdventureWorks**:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Compreendendo as transformações síncronas e assíncronas](~/integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 [Criar uma transformação assíncrona com o componente de Script](~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 [Desenvolvendo um componente de transformação personalizado com saídas síncronas](~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)
 
