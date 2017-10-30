---
title: Configurando o componente Script no Editor de componente de Script | Microsoft Docs
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
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8488fcc7d402430f66b9b9018b31956a5a1d8383
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Configurando o componente Script no Editor de Componentes de Script
  Antes de escrever código personalizado no componente Script, você deve selecionar o tipo de componente de fluxo de dados que você deseja criar — origem, transformação ou destino — e, em seguida, configure os metadados e propriedades do componente de **Editor de transformação scripts**.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Selecionando o tipo de componente a ser criado  
 Quando você adiciona um componente Script ao painel fluxo de dados do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, o **Selecionar tipo de componente de Script** caixa de diálogo é exibida. Pré-configure o componente como uma origem, transformação ou destino. Depois de fazer essa seleção inicial, você pode continuar a configurar o componente no **Editor de transformação scripts**.  
  
 Para definir a linguagem de script padrão para o componente Script, use o **linguagem de script** opção o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
## <a name="understanding-the-two-design-time-modes"></a>Compreendendo os dois modos de tempo de design  
 No [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, o componente Script tem dois modos: modo de design de metadados e modo de design de código.  
  
 Quando você abre o **Editor de transformação scripts**, o componente insere o modo de design de metadados. Nesse modo, você pode selecionar colunas de entrada, e adicionar ou configurar saídas e colunas de saída, mas não pode escrever código. Depois de configurar os metadados do componente, você poderá alternar para o modo de design de código para escrever o script.  
  
 Quando você alterna para o modo de design de código, clicando em **Editar Script**, o componente Script bloqueia metadados para impedir alterações adicionais e, em seguida, gera automaticamente o código base dos metadados das entradas e saídas. Depois que o código gerado automaticamente estiver concluído, você poderá digitar seu código personalizado. Seu código usa as classes base geradas automaticamente para processar linhas de entrada, acessar buffers e colunas nos buffers, além de recuperar gerenciadores de conexões e variáveis do pacote, tudo como objetos fortemente tipados.  
  
 Depois de digitar seu código personalizado em modo de design de código, você pode alternar para o modo de design de metadados. Isso não exclui códigos digitados; porém, as alterações subsequentes nos metadados levam à regeneração da classe base. Posteriormente, a validação de seu componente poderá falhar porque os objetos referenciados por seu código personalizado não existem mais ou foram modificados. Nesse caso, corrija o código manualmente para permitir sua compilação com êxito em relação à classe base regenerada.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Configurando o componente em modo do design de metadados  
 No modo do design de metadados, você pode selecionar colunas de entrada, e adicionar e configurar saídas e colunas de saída, mas não pode escrever código. Depois de configurar os metadados do componente, alterne para o modo de design de código para escrever o script.  
  
 As propriedades a serem configuradas no editor personalizado dependem do uso do componente Script. O componente Script pode ser configurado como uma origem, uma transformação ou um destino. Dependendo de como o componente é usado, ele oferece suporte a uma entrada ou saídas, ou ambas. O código personalizado que você escreverá processa as linhas e colunas de entrada e saída.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Página Colunas de Entrada do Editor de Transformação Scripts  
 O **colunas de entrada** página do **Editor de transformação scripts** é exibida para transformações e destinos, mas não para origens. Nessa página, você seleciona as colunas de entrada disponíveis a serem disponibilizadas para seu script personalizado, e especifica o acesso somente leitura ou de leitura/gravação a elas.  
  
 No projeto de código que será gerado com base nesses metadados, o item de projeto BufferWrapper contém uma classe para cada entrada. Essa classe contém propriedades de acessador tipado para cada coluna de entrada selecionada. Por exemplo, se você selecionar um número inteiro **CustomerID** coluna e uma cadeia de caracteres **CustomerName** coluna a partir de uma entrada denominada **CustomerInput**, o item de projeto BufferWrapper conterá uma **CustomerInput** classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>e o **CustomerInput** classe expõe uma propriedade de inteiro nomeada **CustomerID** e uma propriedade de cadeia de caracteres denominada **CustomerName**. Essa convenção permite escrever código com verificação de tipo, conforme mostrado a seguir:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Para obter mais informações sobre como configurar colunas de entrada para um tipo específico de componente de fluxo de dados, consulte o exemplo apropriado em [desenvolvendo específico Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Página Entradas e Saídas do Editor de Transformação Scripts  
 O **entradas e saídas** página do **Editor de transformação scripts** é exibida para origens, transformações e destinos. Nessa página, você adiciona, remove e configura entradas, saídas e colunas de saída a serem usadas no seu script personalizado, dentro das seguintes limitações:  
  
-   Quando usado como uma origem, o componente Script não possui entrada e dá suporte a várias saídas.  
  
-   Quando usado como uma transformação, o componente Script dá suporte a uma entrada e a várias saídas.  
  
-   Quando usado como um destino, o componente Script dá suporte a uma entrada e não possui saídas.  
  
 No projeto de código que será gerado com base nesses metadados, o item de projeto BufferWrapper contém uma classe para cada entrada e saída. Por exemplo, se você criar uma saída nomeada **CustomerOutput**, o item de projeto BufferWrapper conterá uma **CustomerOutput** classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>e o **CustomerOutput** classe conterá propriedades de acessador tipado para cada coluna de saída criado.  
  
 Você pode configurar colunas de saída somente o **entradas e saídas** página. Você pode selecionar colunas de entrada de transformações e destinos no **colunas de entrada** página. As propriedades de acessador tipado criadas para você no item de projeto BufferWrapper serão somente para gravação em colunas de saída. As propriedades de acessador para colunas de entrada serão somente leitura ou leitura/gravação, dependendo do tipo de uso que você selecionou para cada coluna no **colunas de entrada** página.  
  
 Para obter mais informações sobre como configurar entradas e saídas para um tipo específico de dados de componente de fluxo consulte o exemplo apropriado em [desenvolvendo específico Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Embora não seja possível configurar diretamente uma saída como uma saída de erro no componente Script para manipular automaticamente as linhas de erro, você pode reproduzir a funcionalidade de uma saída de erro criando uma saída adicional e usando o script para direcionar linhas a essa saída quando apropriado. Para obter mais informações, consulte [simulando uma saída de erro para o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Propriedades de saída ExclusionGroup e SynchronousInputID  
 O **ExclusionGroup** propriedade tem um valor diferente de zero somente em transformações com saídas síncronas, onde seu código executa filtragem ou cria ramificações e direciona cada linha em uma das saídas que compartilham o mesmo diferente de zero **ExclusionGroup** valor. Por exemplo, a transformação pode direcionar linhas para a saída padrão ou para uma saída de erro. Quando você criar saídas adicionais para este cenário, certifique-se de definir o valor da **SynchronousInputID** propriedade para o inteiro que corresponde a **ID** de entrada do componente.  
  
 O **SynchronousInputID** propriedade tem um valor diferente de zero somente em transformações com saídas síncronas. Se o valor dessa propriedade for zero, significa que a saída é assíncrona. Para uma saída síncrona, em que linhas são passadas para a saída selecionada ou saídas sem adicionar novas linhas, essa propriedade deve conter o **ID** de entrada do componente.  
  
> [!NOTE]  
>  Quando o **Editor de transformação scripts** cria a primeira saída, ele define o **SynchronousInputID** propriedade de saída para o **ID** de entrada do componente. No entanto, quando o editor cria saídas subsequentes, o editor define o **SynchronousInputID** propriedades dessas saídas como zero.  
>   
>  Se você estiver criando um componente com saídas síncronas, cada saída deverá ter sua **SynchronousInputID** propriedade definida como o **ID** de entrada do componente. Portanto, cada saída criada pelo editor depois que a primeira saída deve ter seu **SynchronousInputID** alterado do valor de zero para o **ID** de entrada do componente.  
>   
>  Se você estiver criando um componente com saídas assíncronas, cada saída deverá ter sua **SynchronousInputID** propriedade definida como zero. Portanto, a primeira saída deve ter seu **SynchronousInputID** alterado do valor da **ID** de entrada do componente para zero.  
  
 Para obter um exemplo de como direcionar linhas para uma das duas saídas síncronas no componente Script, consulte [criando uma transformação síncrona com o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Nomes de objeto em script gerado  
 O componente Script analisa os nomes de entradas e saídas, além dos nomes de colunas nas entradas e saídas. Com base nesses nomes, ele gera classes e propriedades no item de projeto BufferWrapper. Se os nomes encontrados incluírem caracteres que não pertencem às categorias Unicode **UppercaseLetter**, **LowercaseLetter**, **TitlecaseLetter**, **ModifierLetter**, **OtherLetter**, ou **DecimalDigitLetter**, os caracteres inválidos são descartados nos nomes gerados. Por exemplo, espaços são descartados, portanto, duas colunas que têm os nomes de entrada **FirstName** e [**nome**] são interpretadas como ambas contendo o nome da coluna **FirstName**, com resultados imprevisíveis. Para evitar essa situação, os nomes das entradas e saídas e das colunas de entrada e saída usados pelo componente Script devem conter apenas caracteres nas categorias Unicode listadas nessa seção.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Página Script do Editor de Transformação Scripts  
 No **Script** página do **Editor da tarefa Script**, atribua um nome exclusivo e uma descrição para a tarefa de Script. Você também pode atribuir valores para as propriedades a seguir.  
  
> [!NOTE]  
>  No [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e versões posteriores, todos os scripts são pré-compilados. Nas versões anteriores, você especificou se os scripts eram pré-compilados definindo uma **Precompile** propriedade para a tarefa.  
  
#### <a name="validateexternalmetadata-property"></a>Propriedade ValidateExternalMetadata  
 O valor booliano de **propriedade ValidateExternalMetadata** propriedade especifica se o componente deve executar a validação em relação a fontes de dados externas em tempo de design, ou se ele deve adiar a validação até o tempo de execução. Por padrão, o valor dessa propriedade é **True**; ou seja, os metadados externos é validado no tempo de design e em tempo de execução. Você talvez queira definir o valor dessa propriedade como **False** quando uma fonte de dados externa não está disponível em tempo de design: por exemplo, quando o pacote baixa a origem ou cria o destino apenas em tempo de execução.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propriedades ReadOnlyVariables e ReadWriteVariables  
 Você pode inserir listas de variáveis existentes, delimitadas por vírgulas, como os valores dessas propriedades a fim de disponibilizar as variáveis para acesso somente leitura ou leitura/gravação dentro do código de componente Script. Variáveis são acessadas em código através das propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> da classe base gerada automaticamente. Para obter mais informações, consulte [usando variáveis no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 Você pode selecionar o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# como a linguagem de programação do componente Script.  
  
#### <a name="edit-script-button"></a>Botão Editar Script  
 O **Editar Script** botão abre a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE no qual você escreve seu script personalizado. Para obter mais informações, consulte [codificando e depurando o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Página Gerenciadores de Conexões do Editor de Transformação Scripts  
 No **gerenciadores de Conexão** página do **Editor de transformação scripts**, você adiciona e remove gerenciadores de conexão que você deseja usar no seu script personalizado. Em geral, você precisa referenciar gerenciadores de conexões quando cria um componente de origem ou destino.  
  
 No código do projeto que será gerado com base nesses metadados, o **ComponentWrapper** item de projeto contém um **conexões** classe de coleção que tem uma propriedade de acessador tipado para cada Gerenciador de conexão selecionado. Cada propriedade de acessador tipado possui nome idêntico ao do próprio gerenciador de conexões e retorna uma referência ao gerenciador de conexões como uma instância de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por exemplo, se você adicionou um Gerenciador de conexão nomeado `MyADONETConnection` no **gerenciadores de Conexão** página do editor, você pode obter uma referência para o Gerenciador de conexão em seu script usando o código a seguir:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Para obter mais informações, consulte [se conectar a fontes de dados no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Codificando e depurando o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

