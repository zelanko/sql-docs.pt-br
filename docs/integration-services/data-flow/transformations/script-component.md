---
title: Componente Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2c446fd57d8dc795931bf9ff5dba6816ec9c9a57
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="script-component"></a>Componente Script
  O componente Script hospeda o script e permite que um pacote inclua e execute um código de script personalizado. Você pode usar o componente Script em pacotes para as seguintes finalidades:  
  
-   Aplicar várias transformações a dados em vez de usar transformações múltiplas no fluxo de dados. Por exemplo, um script pode adicionar os valores em duas colunas e depois calcular a média da soma.  
  
-   Acessar regras de negócio em um assembly .NET existente. Por exemplo, um script pode aplicar uma regra de negócio que especifica um intervalo de valores válidos em uma coluna **Income** .  
  
-   Usar fórmulas e funções personalizadas além das funções e dos operadores fornecidas pela gramática de expressão do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Por exemplo, validar números de cartão de crédito que usam a fórmula de LUHN.  
  
-   Validar dados de coluna e ignorar registros que contêm dados inválidos. Por exemplo, um script pode avaliar a racionalidade de um valor de postagem e ignorar registros com quantias extremamente altas ou baixas.  
  
 O componente Script fornece um modo fácil e rápido para incluir funções personalizadas em um fluxo de dados. Porém, se você planeja reutilizar o código de script em vários pacotes, deveria considerar programação de componente personalizado em vez de usar o componente Script. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
> [!NOTE]  
>  Se o componente Script contiver um script que tenta ler o valor de uma coluna que é NULL, esse componente falhará quando você executar o pacote. Recomendamos que o script use o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> para determinar se a coluna é NULL antes de tentar ler o valor da coluna.  
  
 O componente Script pode ser usado como uma origem, uma transformação ou um destino. Esse componente oferece suporte a uma entrada e várias saídas. Dependendo de como o componente é usado, ele oferece suporte a uma entrada ou saídas, ou ambas. O script é invocado por toda linha na entrada ou saída.  
  
-   Se usado como origem, o componente Script oferece suporte a várias saídas.  
  
-   Se usado como transformação, o componente Script oferece suporte a uma entrada e a várias saídas.  
  
-   Se usado como destino, o componente Script oferece suporte a uma entrada.  
  
 O componente Script não oferece suporte a saídas de erro.  
  
 Depois de decidir que o componente Script é a escolha adequada para seu pacote, você precisa configurar as entradas e saídas, desenvolver o script usado pelo componente e configurar o próprio componente.  
  
## <a name="understanding-the-script-component-modes"></a>Compreendendo os modos do componente Script  
 No Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , o componente Script tem dois modos: modo do design de metadados e modo do design de código. No modo design de metadados, você pode adicionar e modificar as entradas e saídas do componente Script, mas não pode escrever código. Depois que todas as entradas e saídas são configuradas, você troca para o modo do design de código para escrever o script. O componente Script gera automaticamente o código base a partir dos metadados das entradas e saídas. Se você alterar os metadados depois que o componente Script gerar o código base, talvez seu código não seja compilado porque o código base atualizado pode ser incompatível com seu código.  
  
## <a name="writing-the-script-that-the-component-uses"></a>Escrevendo o Script que o componente usa  
 O componente Script usa o VSTA ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) como o ambiente em que os scripts são gravados. Você acessa o VSTA no **Editor de Transformação Scripts**. Para obter mais informações, consulte [Editor de Transformação Scripts &#40;Página Script&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 O componente Script fornece um projeto VSTA que inclui uma classe gerada automaticamente, nomeada ScriptMain, que representa os metadados do componente. Por exemplo, se o componente Script for usado como uma transformação que tem três saídas, o ScriptMain incluirá um método para cada saída. O ScriptMain é o ponto de entrada para o script.  
  
 O VSTA inclui todos os recursos padrão do ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] , como o editor [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] codificado por cor, o IntelliSense e o Object Browser. O script usado pelo componente Script é armazenado na definição de pacote. Quando você está projetando o pacote, o código de script é gravado temporariamente em um arquivo de projeto.  
  
 O VSTA dá suporte às linguagens de programação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Para obter informações sobre como programar o componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md). Para obter mais informações específicas sobre como configurar o componente Script como origem, transformação ou destino, consulte [Developing Specific Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Para obter exemplos adicionais como um destino de ODBC que demonstra o uso do componente Script, consulte [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  Ao contrário das versões anteriores em que você podia indicar se os scripts eram pré-compilados, todos os scripts são pré-compilados no [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e em versões posteriores. Quando um script é pré-compilado, o mecanismo de linguagem não é carregado no tempo de execução e o pacote é executado mais rapidamente. No entanto, arquivos binários pré-compilados consomem espaço significativo em disco.  
  
## <a name="configuring-the-script-component"></a>Configurando o componente Script  
 Você pode configurar o componente Script das seguintes maneiras:  
  
-   Selecione as colunas de entrada para referência.  
  
    > [!NOTE]  
    >  Você pode configurar só uma entrada quando usar o Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
-   Forneça o script que o componente é executado.  
  
-   Especifique a linguagem do script.  
  
-   Forneça listas separadas por vírgula das variáveis de somente leitura e gravação/leitura.  
  
-   Adicione mais saídas e adicione colunas de saída atribuídas ao script.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>Configurando o componente Script no Designer  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Configurando o componente Script programaticamente  
 Para obter mais informações sobre as propriedades que podem ser definidas na janela **Propriedades** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>Selecionar Tipo de Componente do Script
  Use a caixa de diálogo **Selecionar Tipo de Componente do Script** para especificar se deve ser criada uma Transformação Scripts pré-configurada para uso como origem, transformação ou destino.  
  
 Para obter mais informações sobre o componente Script, consulte [Configurar o componente Script no Editor de Componentes Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opções  
 Sua seleção de **Origem**, **Destino**ou **Transformação** afeta a configuração da Transformação Scripts e as páginas do Editor de Transformação Scripts.  
  
## <a name="script-transformation-editor-connection-managers-page"></a>Editor de Transformação Scripts (página Gerenciadores de Conexões)
  Use a página **Gerenciadores de Conexões** do **Editor de Transformação Scripts** para especificar as conexões que serão usadas pelo script.  
  
 Para obter mais informações sobre o componente Script, consulte [Configurar o componente Script no Editor de Componentes Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opções  
 **Connection managers**  
 Exiba a lista de conexões disponíveis para serem usadas pelo script.  
  
 **Nome**  
 Digite um nome exclusivo e descritivo para a conexão.  
  
 **Gerenciador de Conexões**  
 Selecione na lista de gerenciadores de conexões disponíveis ou selecione **\<Nova conexão>** para abrir a caixa de diálogo **Adicionar Gerenciador de Conexões SSIS**.  
  
 **Descrição**  
 Digite uma descrição para a conexão.  
  
 **Adicionar**  
 Adicione outra conexão à lista **Gerenciadores de conexões** .  
  
 **Remover**  
 Remova a conexão selecionada da lista **Gerenciadores de conexões** .  
  
## <a name="script-transformation-editor-input-columns-page"></a>Editor de Transformação Scripts (página Colunas de Entrada)
  Use a página **Colunas de Entrada** da caixa de diálogo **Editor de Transformação Scripts** para definir propriedades nas colunas de entrada.  
  
> [!NOTE]  
>  A página **Colunas de Entrada** não é exibida para componentes de Origem que têm saídas mas não têm entradas.  
  
 Para obter mais informações sobre o componente Script, consulte [Configurar o componente Script no Editor de Componentes Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opções  
 **Nome de entrada**  
 Selecione na lista de entradas disponíveis.  
  
 **Colunas de Entrada Disponíveis**  
 Usando as caixas de seleção, especifique as colunas que a transformação scripts usará.  
  
 **Coluna de Entrada**  
 Selecione colunas para cada linha na lista de colunas de entrada disponíveis. As seleções se refletem naquelas da caixa de seleção da tabela **Colunas de Entrada Disponíveis**.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Tipo de Uso**  
 Especifique se a Transformação Scripts tratará cada coluna como **ReadOnly** ou **ReadWrite**.  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>Editor de Transformação Scripts (página Entradas e Saídas)
  Use a página **Entradas e Saídas** da caixa de diálogo do **Editor de Transformação Scripts** para adicionar, remover e configurar entradas e saídas para a Transformação Scripts.  
  
> [!NOTE]  
>  Os componentes de origem possuem saídas e não entradas, enquanto os componentes de destino possuem entradas mas nenhuma saída. Transformações têm entradas e saídas.  
  
 Para obter mais informações sobre o componente Script, consulte [Configurar o componente Script no Editor de Componentes Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opções  
 **Inputs and outputs**  
 Selecione uma entrada ou uma saída à esquerda para exibir suas propriedades na tabela à direita. As propriedades disponíveis para edição variam de acordo com a seleção. Muitas das propriedades exibidas são somente leitura. Para obter mais informações sobre as propriedades individuais, consulte os tópicos abaixo.  
  
 [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **Adicionar Saída**  
 Adicione uma saída adicional à lista.  
  
 **Adicionar Coluna**  
 Selecione uma pasta na qual deseja colocar a nova coluna de saída e adicione a coluna clicando em **Adicionar Coluna**.  
  
 **Remover Saída**  
 Selecione uma saída e remova-a clicando em **Remover Saída**.  
  
 **Remover Coluna**  
 Selecione uma coluna e remova-a clicando em **Remover Coluna**.  
  
## <a name="script-transformation-editor-script-page"></a>Editor de Transformação Scripts (página Script)
  Use a guia **Script** da caixa de diálogo **Editor de Transformação Scripts** para especificar um script e propriedades relacionadas.  
  
 Para obter mais informações sobre o componente Script, consulte [Configurar o componente Script no Editor de Componentes Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opções  
 **Propriedades**  
 Visualize e modifique as propriedades da transformação Scripts. Muitas das propriedades exibidas são somente leitura. Você pode modificar as seguintes propriedades:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Descrição**|Descreva a finalidade da transformação scripts.|  
|**LocaleID**|Especifique a localidade para fornecer informações de solicitação e de conversão de data e hora específicas da região.|  
|**Nome**|Digite um nome descritivo para o componente.|  
|**ValidateExternalMetadata**|Indique se a transformação Scripts deve validar coluna de metadados contra fontes de dados externas em tempo de design. Um valor de **false** retarda a validação até o momento da execução.|  
|**ReadOnlyVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo somente leitura pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ReadWriteVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo leitura/gravação pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ScriptLanguage**|Selecione a linguagem de script a ser usada pelo componente de Script.<br /><br /> Para definir a linguagem de script padrão para componentes e tarefas de Script, use a opção **Linguagem de script** na página **Geral** da caixa de diálogo **Opções** .|  
|**UserComponentTypeName**|Especifica a classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> e o assembly **Microsoft.SqlServer.TxScript** que dá suporte à infraestrutura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 **Editar Script**  
 Use o VSTA [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] (Tools for Applications) para criar ou modificar um script.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  
