---
title: Configurando o componente Script no Editor de Componentes de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b2b588c61742d5ab9c57d934b0f4f11230f1ca5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894810"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Configurando o componente Script no Editor de Componentes de Script
  Antes de escrever um código personalizado no componente Script, primeiro selecione o tipo de componente de fluxo de dados que deseja criar – origem, transformação ou destino – e, em seguida, configure os metadados e as propriedades do componente no **Editor de Transformação Scripts**.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Selecionando o tipo de componente a ser criado  
 Quando você adiciona um componente Script ao painel Fluxo de Dados do Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)], a caixa de diálogo **Selecionar Tipo de Componente Script** é exibida. Pré-configure o componente como uma origem, transformação ou destino. Depois de fazer essa seleção inicial, continue configurando o componente no **Editor de Transformação Scripts**.  
  
 Para definir a linguagem de script padrão para o componente Script, use a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](../../general-page-of-integration-services-designers-options.md).  
  
## <a name="understanding-the-two-design-time-modes"></a>Compreendendo os dois modos de tempo de design  
 No [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, o componente Script tem dois modos: modo de design de metadados e modo de design de código.  
  
 Quando você abre o **Editor de Transformação Scripts**, o componente insere o modo de design de metadados. Nesse modo, você pode selecionar colunas de entrada, e adicionar ou configurar saídas e colunas de saída, mas não pode escrever código. Depois de configurar os metadados do componente, você poderá alternar para o modo de design de código para escrever o script.  
  
 Quando você alterna para o modo de design de código clicando em **Editar Script**, o componente Script bloqueia metadados para impedir alterações adicionais e, depois, gera automaticamente o código base dos metadados das entradas e saídas. Depois que o código gerado automaticamente estiver concluído, você poderá digitar seu código personalizado. Seu código usa as classes base geradas automaticamente para processar linhas de entrada, acessar buffers e colunas nos buffers, além de recuperar gerenciadores de conexões e variáveis do pacote, tudo como objetos fortemente tipados.  
  
 Depois de digitar seu código personalizado em modo de design de código, você pode alternar para o modo de design de metadados. Isso não exclui códigos digitados; porém, as alterações subsequentes nos metadados levam à regeneração da classe base. Posteriormente, a validação de seu componente poderá falhar porque os objetos referenciados por seu código personalizado não existem mais ou foram modificados. Nesse caso, corrija o código manualmente para permitir sua compilação com êxito em relação à classe base regenerada.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Configurando o componente em modo do design de metadados  
 No modo do design de metadados, você pode selecionar colunas de entrada, e adicionar e configurar saídas e colunas de saída, mas não pode escrever código. Depois de configurar os metadados do componente, alterne para o modo de design de código para escrever o script.  
  
 As propriedades a serem configuradas no editor personalizado dependem do uso do componente Script. O componente Script pode ser configurado como uma origem, uma transformação ou um destino. Dependendo de como o componente é usado, ele oferece suporte a uma entrada ou saídas, ou ambas. O código personalizado que você escreverá processa as linhas e colunas de entrada e saída.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Página Colunas de Entrada do Editor de Transformação Scripts  
 A página **Colunas de Entrada** do **Editor de Transformação Scripts** é exibida para transformações e destinos, mas não para origens. Nessa página, você seleciona as colunas de entrada disponíveis a serem disponibilizadas para seu script personalizado, e especifica o acesso somente leitura ou de leitura/gravação a elas.  
  
 No projeto de código que será gerado com base nesses metadados, o item de projeto BufferWrapper contém uma classe para cada entrada. Essa classe contém propriedades de acessador tipado para cada coluna de entrada selecionada. Por exemplo, se você selecionar uma coluna **CustomerID** inteiro e uma coluna **CustomerName** de uma entrada chamada `CustomerInput`, o item de projeto BufferWrapper conterá `CustomerInput` uma classe derivada <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>de, e `CustomerInput` a classe irá expor uma propriedade Integer chamada **CustomerID** e uma propriedade String chamada **CustomerName**. Essa convenção permite escrever código com verificação de tipo, conforme mostrado a seguir:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Para obter mais informações sobre como configurar colunas de entrada para um tipo específico de componente de fluxo de dados, consulte o exemplo apropriado em [Desenvolvendo tipos específicos de componentes de Script](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Página Entradas e Saídas do Editor de Transformação Scripts  
 A página **Entradas e Saídas** do **Editor de Transformação Scripts** é exibida para origens, transformações e destinos. Nessa página, você adiciona, remove e configura entradas, saídas e colunas de saída a serem usadas no seu script personalizado, dentro das seguintes limitações:  
  
-   Quando usado como uma origem, o componente Script não possui entrada e dá suporte a várias saídas.  
  
-   Quando usado como uma transformação, o componente Script dá suporte a uma entrada e a várias saídas.  
  
-   Quando usado como um destino, o componente Script dá suporte a uma entrada e não possui saídas.  
  
 No projeto de código que será gerado com base nesses metadados, o item de projeto BufferWrapper contém uma classe para cada entrada e saída. Por exemplo, se você criar uma saída chamada `CustomerOutput`, o item de projeto BufferWrapper conterá `CustomerOutput` uma classe derivada de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, e a `CustomerOutput` classe conterá Propriedades de acessador de tipo para cada coluna de saída criada.  
  
 Você só pode configurar colunas de saída na página **Entradas e Saídas**. Selecione colunas de entrada para transformações e destinos na página **Colunas de Entrada**. As propriedades de acessador tipado criadas para você no item de projeto BufferWrapper serão somente para gravação em colunas de saída. As propriedades do acessador para colunas de entrada serão somente leitura ou de leitura/gravação, dependendo do tipo de uso selecionado para cada coluna na página **Colunas de Entrada**.  
  
 Para obter mais informações sobre como configurar entradas e saídas para um tipo específico de componente de fluxo de dados, consulte o exemplo apropriado em [Desenvolvendo tipos específicos de componentes de Script](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Embora não seja possível configurar diretamente uma saída como uma saída de erro no componente Script para manipular automaticamente as linhas de erro, você pode reproduzir a funcionalidade de uma saída de erro criando uma saída adicional e usando o script para direcionar linhas a essa saída quando apropriado. Para obter mais informações, consulte [Simulando uma saída de erro para o componente Script](../../data-flow/transformations/script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Propriedades de saída ExclusionGroup e SynchronousInputID  
 A propriedade `ExclusionGroup` possui um valor diferente de zero somente em transformações com saídas síncronas, onde seu código executa a filtragem ou cria ramificações e direciona cada linha para uma das saídas que compartilham o mesmo valor `ExclusionGroup` diferente de zero. Por exemplo, a transformação pode direcionar linhas para a saída padrão ou para uma saída de erro. Ao criar saídas adicionais para este cenário, certifique-se de que tenha definido o valor da propriedade `SynchronousInputID` como o inteiro que corresponde ao `ID` da entrada do componente.  
  
 A propriedade `SynchronousInputID` só tem um valor diferente de zero em transformações com saídas síncronas. Se o valor dessa propriedade for zero, significa que a saída é assíncrona. Para uma saída síncrona, em que linhas são transmitidas às saídas selecionadas sem adicionar novas linhas, essa propriedade deve conter a `ID` da entrada do componente.  
  
> [!NOTE]  
>  Quando o **Editor de transformação scripts** cria a primeira saída, o editor define `SynchronousInputID` a propriedade da saída para a `ID` da entrada do componente. Porém, quando o editor cria saídas subsequentes, ele define as propriedades `SynchronousInputID` dessas saídas como zero.  
>   
>  Se você estiver criando um componente com saídas síncronas, cada saída deverá ter `SynchronousInputID` sua propriedade definida como `ID` a da entrada do componente. Portanto, cada saída criada pelo editor depois da primeira saída precisa mudar seu valor `SynchronousInputID` de zero para a `ID` da entrada do componente.  
>   
>  Se você estiver criando um componente com saídas assíncronas, cada saída deverá ter sua propriedade `SynchronousInputID` definida como zero. Portanto, a primeira saída deve ter seu `SynchronousInputID` valor alterado do `ID` da entrada do componente para zero.  
  
 Para obter um exemplo de como direcionar linhas para uma das duas saídas síncronas no componente Script, consulte [Criando uma transformação síncrona com o componente Script](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Nomes de objeto em script gerado  
 O componente Script analisa os nomes de entradas e saídas, além dos nomes de colunas nas entradas e saídas. Com base nesses nomes, ele gera classes e propriedades no item de projeto BufferWrapper. Se os nomes encontrados incluírem caracteres que não pertencem às categorias Unicode `UppercaseLetter`, `LowercaseLetter`, `TitlecaseLetter`, `ModifierLetter`, `OtherLetter` ou `DecimalDigitLetter`, os caracteres inválidos serão descartados nos nomes gerados. Por exemplo, os espaços são removidos; portanto, duas colunas de entrada que têm os nomes **FirstName** e [**First Name**] são interpretadas como tendo o nome de coluna **FirstName**, com resultados imprevisíveis. Para evitar essa situação, os nomes das entradas e saídas e das colunas de entrada e saída usados pelo componente Script devem conter apenas caracteres nas categorias Unicode listadas nessa seção.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Página Script do Editor de Transformação Scripts  
 Na página **Script** do **Editor da Tarefa Script**, atribua um nome exclusivo e uma descrição à tarefa Script. Você também pode atribuir valores para as propriedades a seguir.  
  
> [!NOTE]  
>  No [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e versões posteriores, todos os scripts são pré-compilados. Em versões anteriores, você especificava se os scripts eram pré-compilados definindo uma propriedade `Precompile` para a tarefa.  
  
#### <a name="validateexternalmetadata-property"></a>Propriedade ValidateExternalMetadata  
 O valor booleano da propriedade `ValidateExternalMetadata` especifica se o componente deve executar a validação em relação a fontes de dados externas no tempo de design, ou se ele deve adiar a validação até o tempo de execução. Por padrão, o valor dessa propriedade é `True`; ou seja, os metadados externos são validados em tempo de design e em tempo de execução. Talvez você queira definir o valor dessa propriedade como `False` quando uma fonte de dados externa não está disponível no tempo de design: por exemplo, quando o pacote baixa a origem ou cria o destino apenas em tempo de execução.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propriedades ReadOnlyVariables e ReadWriteVariables  
 Você pode inserir listas de variáveis existentes, delimitadas por vírgulas, como os valores dessas propriedades a fim de disponibilizar as variáveis para acesso somente leitura ou leitura/gravação dentro do código de componente Script. Variáveis são acessadas em código através das propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> da classe base gerada automaticamente. Para obter mais informações, consulte [Usando variáveis no componente Script](using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 Você pode selecionar o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# como a linguagem de programação do componente Script.  
  
#### <a name="edit-script-button"></a>Botão Editar Script  
 O botão **Editar Script** abre o IDE do VSTA ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) no qual você escreve o script personalizado. Para obter mais informações, consulte [Codificando e depurando o componente Script](coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Página Gerenciadores de Conexões do Editor de Transformação Scripts  
 Na página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**, você adiciona e remove gerenciadores de conexões que deseja usar no script personalizado. Em geral, você precisa referenciar gerenciadores de conexões quando cria um componente de origem ou destino.  
  
 No projeto de código que será gerado com base nesses metadados, o item de projeto `ComponentWrapper` contém uma classe de coleção `Connections` que possui uma propriedade de acessador tipado para cada gerenciador de conexões selecionado. Cada propriedade de acessador tipado possui nome idêntico ao do próprio gerenciador de conexões e retorna uma referência ao gerenciador de conexões como uma instância de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por exemplo, se você adicionou um gerenciador de conexões chamado `MyADONETConnection` na página **Gerenciadores de Conexões** do editor, poderá obter uma referência ao gerenciador de conexões no script usando o seguinte código:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Para obter mais informações, consulte [Conectando-se a fontes de dados no componente Script](connecting-to-data-sources-in-the-script-component.md).  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Codificando e depurando o componente Script](coding-and-debugging-the-script-component.md)  
  
  
