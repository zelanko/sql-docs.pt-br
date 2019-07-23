---
title: Estender o fluxo de dados com o componente Script | Microsoft Docs
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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9212c92f05926a3ecb2f3fb8eb02b381e2bb2e47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103990"
---
# <a name="extending-the-data-flow-with-the-script-component"></a>Extending the Data Flow with the Script Component

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente Script estende as capacidades de fluxo de dados dos pacotes [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] com o código personalizado escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# que é compilado e executado no tempo de execução do pacote. O componente Script simplifica o desenvolvimento de uma origem de fluxo de dados personalizada, transformação ou destino quando as origens, transformações e destinos incluídos no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] não atendem totalmente aos seus requisitos. Após a configuração do componente com as entradas e saídas esperadas, ele grava todo o código de infraestrutura necessário, permitindo que você se concentre exclusivamente no código que é exigido para seu processamento personalizado.  
  
 Um componente Script interage com o pacote recipiente e com o fluxo de dados por meio das classes geradas automaticamente nos itens de projeto **ComponentWrapper** e **BufferWrapper**, que são instâncias das classes <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, respectivamente. Essas classes tornam conexões, variáveis e outros itens de pacote disponíveis como objetos com tipo e gerenciam entradas e saídas. O componente Script também pode usar o namespace [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e a biblioteca de classe [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como também assemblies personalizados, para implementar a funcionalidade personalizada.  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. Entretanto, para compreender como o componente Script funciona, pode ser útil ler a seção [Desenvolver um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) para compreender as etapas envolvidas no desenvolvimento de um componente do fluxo de dados personalizado.  
  
 Se estiver criando uma origem, transformação ou destino que planeja reutilizar em vários pacotes, você deverá considerar o desenvolvimento de um componente personalizado em vez de usar o componente Script. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre o componente Script.  
  
 [Configurar o componente de Script no Editor de Componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 As propriedades que você configura no **Editor de Transformação Scripts** afetam a capacidade e o desempenho de código de componente Script.  
  
 [Codificar e depurar o componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 Use o ambiente de desenvolvimento do VSTA ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) para desenvolver os scripts contidos no componente Script.  
  
 [Compreender o Component Object Model do Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Um projeto de componente Script novo contém três itens de projeto com várias classes e propriedades e métodos gerados automaticamente.  
  
 [Usar variáveis no componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 O item de projeto **ComponentWrapper** contém propriedades de acessador fortemente tipadas para variáveis de pacote.  
  
 [Conectar-se a fontes de dados no componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 O item de projeto **ComponentWrapper** também contém propriedades de acessador fortemente tipadas para conexões definidas no pacote.  
  
 [Gerar eventos no componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 Você pode gerar eventos para fornecer notificação de problemas e erros.  
  
 [Registrar o componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 Você pode registrar informações para registrar provedores habilitados no pacote.  
  
 [Desenvolver tipos específicos de componentes de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 Estes exemplos simples explicam e se manifestam como usar o componente Script para desenvolver origens de fluxo de dados, transformações e destinos.  
  
 [Exemplos de componentes de Script adicionais](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 Esses exemplos simples explicam e demonstram alguns possíveis usos para o componente Script.  
  
## <a name="see-also"></a>Consulte Também  
 [Componente Script](../../../integration-services/data-flow/transformations/script-component.md)   
 [Comparar a tarefa Script e o componente de Script](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
