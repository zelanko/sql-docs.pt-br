---
title: Desenvolver tipos específicos de componentes de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78810a0599d2345770175bc0ed9bdc06f3195817
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375384"
---
# <a name="developing-specific-types-of-data-flow-components"></a>Desenvolvendo tipos específicos de componentes de fluxo de dados
  Esta seção aborda as especificações do desenvolvimento de componentes de origem, componentes de transformação com saídas síncronas, componentes de transformação com saídas assíncronas e componentes de destino.  
  
 Para obter informações sobre desenvolvimento de componentes em geral, consulte [Desenvolver um componente de fluxo de dados personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Desenvolvendo um componente de origem personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contém informações sobre o desenvolvimento de um componente que acessa dados de uma fonte de dados externa e fornece-os a componentes downstream no fluxo de dados.  
  
 [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contém informações sobre o desenvolvimento de um componente de transformação cujas saídas são síncronas para suas entradas. Esses componentes não adicionam dados ao fluxo de dados, mas processam dados percorridos.  
  
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contém informações sobre o desenvolvimento de um componente de transformação cujas saídas não são síncronas para suas entradas. Esses componentes recebem dados de componentes upstream, mas também adicionam dados ao fluxo de dados.  
  
 [Desenvolvendo um componente de destino personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contém informações sobre o desenvolvimento de um componente que recebe linhas de componentes upstream no fluxo de dados e grava-as em uma fonte de dados externa.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contém as classes e interfaces usadas para criar componentes de fluxo de dados personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contém as classes não gerenciadas e as interfaces da tarefa de fluxo de dados. O desenvolvedor usa esses elementos e o namespace <xref:Microsoft.SqlServer.Dts.Pipeline> gerenciado quando cria um fluxo de dados programaticamente ou cria componentes de fluxo de dados personalizados.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar soluções de script e objetos personalizados](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desenvolver tipos específicos de componentes de Script](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
