---
title: "Componente Script | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.scriptcomponentdetails.f1"
helpviewer_keywords: 
  - "Transformação Script"
  - "scripts [Integration Services], transformações"
  - "Componente de script [Integration Services], sobre o componente Script"
  - "componente Script [Integration Services]"
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 70
---
# Componente Script
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
  
## Compreendendo os modos do componente Script  
 No Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)], o componente Script tem dois modos: modo do design de metadados e modo do design de código. No modo design de metadados, você pode adicionar e modificar as entradas e saídas do componente Script, mas não pode escrever código. Depois que todas as entradas e saídas são configuradas, você troca para o modo do design de código para escrever o script. O componente Script gera automaticamente o código base a partir dos metadados das entradas e saídas. Se você alterar os metadados depois que o componente Script gerar o código base, talvez seu código não seja compilado porque o código base atualizado pode ser incompatível com seu código.  
  
## Escrevendo o Script que o componente usa  
 O componente Script usa o VSTA ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) como o ambiente em que os scripts são gravados. Você acessa o VSTA no **Editor de Transformação Scripts**. Para obter mais informações, consulte [Editor de Transformação Scripts &#40;página Script&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 O componente Script fornece um projeto VSTA que inclui uma classe gerada automaticamente, nomeada ScriptMain, que representa os metadados do componente. Por exemplo, se o componente Script for usado como uma transformação que tem três saídas, o ScriptMain incluirá um método para cada saída. O ScriptMain é o ponto de entrada para o script.  
  
 O VSTA inclui todos os recursos padrão do ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], como o editor [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] codificado por cor, o IntelliSense e o Object Browser. O script usado pelo componente Script é armazenado na definição de pacote. Quando você está projetando o pacote, o código de script é gravado temporariamente em um arquivo de projeto.  
  
 O VSTA dá suporte às linguagens de programação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Para obter informações sobre como programar o componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md). Para obter mais informações específicas sobre como configurar o componente Script como origem, transformação ou destino, consulte [Developing Specific Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Para obter exemplos adicionais como um destino de ODBC que demonstra o uso do componente Script, consulte [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  Ao contrário das versões anteriores em que você podia indicar se os scripts eram pré-compilados, todos os scripts são pré-compilados no [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e em versões posteriores. Quando um script é pré-compilado, o mecanismo de linguagem não é carregado no tempo de execução e o pacote é executado mais rapidamente. No entanto, arquivos binários pré-compilados consomem espaço significativo em disco.  
  
## Configurando o componente Script  
 Você pode configurar o componente Script das seguintes maneiras:  
  
-   Selecione as colunas de entrada para referência.  
  
    > [!NOTE]  
    >  Você pode configurar só uma entrada quando usar o Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
-   Forneça o script que o componente é executado.  
  
-   Especifique a linguagem do script.  
  
-   Forneça listas separadas por vírgula das variáveis de somente leitura e gravação/leitura.  
  
-   Adicione mais saídas e adicione colunas de saída atribuídas ao script.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
### Configurando o componente Script no Designer  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Scripts** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Scripts &#40;página Colunas de Entrada&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)  
  
-   [Editor de Transformação Scripts &#40;Página Entradas e Saídas&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [Editor de Transformação Scripts &#40;Página Script&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)  
  
-   [Editor de Transformação Scripts &#40;Página Gerenciadores de Conexões&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### Configurando o componente Script programaticamente  
 Para obter mais informações sobre as propriedades que podem ser definidas na janela **Propriedades** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Conteúdo relacionado  
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Estendendo o fluxo de dados com o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  