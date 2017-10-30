---
title: Estendendo o fluxo de dados com o componente Script | Microsoft Docs
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
- data flow task [Integration Services], components
- data flow [Integration Services], extending
- debugging [Integration Services], components
- code design mode [Integration Services]
- metadata [Integration Services]
- scripts [Integration Services], extending data flow
- data flow components [Integration Services], Script component
- components [Integration Services], data flow
- Script component [Integration Services], about Script component
- Script component [Integration Services]
- data flow [Integration Services], components
ms.assetid: 072bc4b8-363a-4131-87c3-240338e2fa5c
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c58a854082fcbd12333be63995e4fcdf2d55aac7
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-data-flow-with-the-script-component"></a>Extending the Data Flow with the Script Component
  O componente Script estende as capacidades de fluxo de dados de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] pacotes com código personalizado escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual c# que é compilado e executado no tempo de execução do pacote. O componente Script simplifica o desenvolvimento de uma origem de fluxo de dados personalizada, transformação ou destino quando as origens, transformações e destinos incluídos no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] não atendem totalmente aos seus requisitos. Após a configuração do componente com as entradas e saídas esperadas, ele grava todo o código de infraestrutura necessário, permitindo que você se concentre exclusivamente no código que é exigido para seu processamento personalizado.  
  
 Um componente Script interage com o pacote de conteúdo e o fluxo de dados por meio das classes geradas automaticamente no **ComponentWrapper** e **BufferWrapper** itens, que são instâncias de projeto do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> classes respectivamente. Essas classes tornam conexões, variáveis e outros itens de pacote disponíveis como objetos com tipo e gerenciam entradas e saídas. O componente Script também pode usar o namespace [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e a biblioteca de classe [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como também assemblies personalizados, para implementar a funcionalidade personalizada.  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler a seção [desenvolvendo um componente de fluxo de dados personalizada](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) para compreender as etapas envolvidas no desenvolvimento de um componente de fluxo de dados personalizado.  
  
 Se estiver criando uma origem, transformação ou destino que planeja reutilizar em vários pacotes, você deverá considerar o desenvolvimento de um componente personalizado em vez de usar o componente Script. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre o componente Script.  
  
 [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 Propriedades que você configurar o **Editor de transformação scripts** afetam a capacidade e o desempenho do código do componente Script.  
  
 [Codificando e depurando o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 Você usa o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ferramentas para ambiente de desenvolvimento de aplicativos (VSTA) para desenvolver os scripts contidos no componente Script.  
  
 [Noções básicas sobre o modelo de objeto do componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Um projeto de componente Script novo contém três itens de projeto com várias classes e propriedades e métodos gerados automaticamente.  
  
 [Usando variáveis no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 O **ComponentWrapper** item de projeto contém propriedades de acessador fortemente tipadas para variáveis de pacote.  
  
 [Conectando-se a fontes de dados no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 O **ComponentWrapper** item de projeto também contém propriedades de acessador fortemente tipadas para conexões definidas no pacote.  
  
 [Gerando eventos no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 Você pode gerar eventos para fornecer notificação de problemas e erros.  
  
 [Registro em log no componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 Você pode registrar informações para registrar provedores habilitados no pacote.  
  
 [Desenvolvendo tipos específicos de componentes de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 Estes exemplos simples explicam e se manifestam como usar o componente Script para desenvolver origens de fluxo de dados, transformações e destinos.  
  
 [Exemplos de componentes Script adicionais](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 Esses exemplos simples explicam e demonstram alguns possíveis usos para o componente Script.  
  
## <a name="see-also"></a>Consulte também  
 [Componente de script](../../../integration-services/data-flow/transformations/script-component.md)   
 [Comparando a tarefa de Script e o componente Script](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  

