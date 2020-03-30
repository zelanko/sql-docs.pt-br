---
title: Desenvolvendo objetos personalizados para o Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b621ebd5750d918c22f61ac005b02e1b8bea187
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297212"
---
# <a name="developing-custom-objects-for-integration-services"></a>Desenvolvendo objetos personalizados para o Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando os objetos de fluxo de controle e de fluxo de dados incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não atendem completamente a seus requisitos, você pode desenvolver muitos tipos de objetos personalizados, incluindo:  
  
-   **Tarefas personalizadas**.  
  
-   **Gerenciadores de conexões personalizados.** Conectam-se a fontes de dados externas sem-suporte atualmente.  
  
-   **Provedores de log personalizados.** Registram eventos de pacote em formatos sem-suporte atualmente.  
  
-   **Enumeradores personalizados.** Dão suporte à iteração de um conjunto de formatos de objetos ou valores sem-suporte atualmente.  
  
-   **Componentes de fluxo de dados personalizados.** Podem ser configurados como origens, transformações ou destinos.  
  
 O modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] facilita esse desenvolvimento personalizado com classes base que fornecem uma estrutura consistente e confiável para sua implementação personalizada.  
  
 Se você não tiver que reutilizar a funcionalidade personalizada em múltiplos pacotes, a tarefa Script e o componente Script proporcionam o total poder de uma linguagem de programação gerenciada, com significativamente menos códigos de infraestrutura para gravar. Para obter mais informações, consulte [Comparar soluções de script e objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Etapas para desenvolver um objeto personalizado para o Integration Services  
 Quando você desenvolve um objeto personalizado para usar no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você desenvolve uma Biblioteca de Classes (DLL) que será carregada em tempo de design e em runtime pelo SSIS Designer e pelo runtime do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Os métodos mais importantes que você deve implementar não são métodos que você chama do seu próprio código, mas métodos que o runtime chama em momentos apropriados para inicializar e validar seu componente e invocar sua funcionalidade.  
  
 Eis as etapas que você deve seguir para desenvolver um objeto personalizado:  
  
1.  Crie um projeto novo do tipo Biblioteca de Classes na linguagem de programação gerenciada de sua preferência.  
  
2.  Herde da classe base apropriada, como mostrado na tabela seguinte.  
  
3.  Aplique o atributo apropriado em sua classe nova, como mostrado na tabela seguinte.  
  
4.  Substitua os métodos da classe base, conforme requerido, e grave o código para a funcionalidade personalizada de seu objeto.  
  
5.  Opcionalmente, compile uma interface do usuário personalizada para seu componente. Para facilitar a implantação, talvez você queira desenvolver a interface do usuário como um projeto separado na mesma solução e compilá-lo como um assembly separado.  
  
6.  Opcionalmente, exiba um link para exemplos e conteúdo da Ajuda para o objeto personalizado, na **Caixa de ferramentas do SSIS**.  
  
7.  Crie, implante e depure seu novo objeto personalizado conforme descrito em [Compilar, implantar e depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="base-classes-attributes-and-important-methods"></a>Classes base, atributos e métodos importantes  
 Esta tabela fornece uma referência fácil aos elementos mais importantes no modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para cada tipo de objeto personalizado que você pode desenvolver.  
  
|Objeto personalizado|Classe base|Atributo|Métodos importantes|  
|-------------------|----------------|---------------|-----------------------|  
|Tarefa|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|Gerenciador de conexões|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|Provedor de log|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|Enumerador|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|Componente de fluxo de dados|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>Fornecendo links para exemplos e conteúdo da ajuda  
 Para exibir um link na **Caixa de Ferramentas do SSIS** para exemplos e conteúdo da Ajuda para um objeto personalizado escrito em código gerenciado, use as propriedades a seguir.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 Para exibir um link para exemplos e conteúdo da Ajuda para um objeto personalizado escrito em código nativo, adicione entradas no arquivo de Script de Registro (.rgs) para SamplesTag, HelpKeyword e HelpCollection. A seguir, é mostrado um exemplo.  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>Fornecendo uma interface do usuário personalizada  
 Para permitir que os usuários de seu objeto personalizado configurem suas propriedades, você pode ser necessário desenvolver uma interface do usuário personalizada. Nos casos em que uma interface do usuário personalizada não for estritamente necessária, você pode escolher criar uma para fornecer uma interface mais amigável do que o editor padrão.  
  
 Em um projeto ou assembly de interface do usuário personalizada, normalmente você tem duas classes – uma classe que implementa uma interface do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para interfaces do usuário para o tipo específico de objeto personalizado e o formulário do Windows exibido para reunir informações do usuário. As interfaces que você implementa têm somente alguns métodos e uma interface do usuário personalizada não é difícil desenvolver.  
  
> [!NOTE]  
>  Muitos provedores de log do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] têm uma interface do usuário personalizada que implementa o <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e substitui a caixa de texto **Configuração** por uma lista suspensa filtrada com gerenciadores de conexões disponíveis. Porém, interfaces do usuário personalizadas não são implementadas para provedores de log personalizados nesta versão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Especificar um valor para a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> não tem efeito.  
  
 A tabela a seguir fornece uma referência fácil às interfaces que você deve implementar quando desenvolve uma interface do usuário personalizada para cada tipo de objeto personalizado. Ela também explica o que o usuário vê se você decide não desenvolver uma interface do usuário personalizada para seu objeto ou se você deixa de vincular seu objeto à sua interface do usuário usando a propriedade **UITypeName** no atributo do objeto. Embora o potente Editor Avançado possa ser satisfatório para um componente de fluxo de dados, a janela Propriedades é uma solução menos amigável para tarefas e gerenciadores de conexões, e um enumerador de Foreach personalizado não pode ser configurado sem um formulário personalizado.  
  
|Objeto personalizado|Classe base para interface do usuário|Comportamento de edição padrão se nenhuma interface do usuário personalizada é fornecida|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|Tarefa|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|Somente a janela Propriedades|  
|Gerenciador de conexões|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|Somente a janela Propriedades|  
|Provedor de log|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> (Não implementado no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)])|Caixa de texto na coluna **Configuração**|  
|Enumerador|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|Somente a janela Propriedades. A área Configuração do Enumerador do editor está vazia.|  
|Componente de fluxo de dados|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|Editor Avançado|  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [O processo de criação de solução do Visual Studio dá um aviso sobre a dependência indireta no assembly do .NET Framework devido a referências SSIS](https://go.microsoft.com/fwlink/?LinkId=215662), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Compilando, implantando e depurando objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  
