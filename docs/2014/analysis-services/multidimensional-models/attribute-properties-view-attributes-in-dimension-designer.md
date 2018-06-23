---
title: Exibir atributos no Designer de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c78e76030fe216df9e610b0e1ab6e6f37a652b30
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010114"
---
# <a name="view-attributes-in-dimension-designer"></a>Exibir atributos no Designer de Dimensão
  São criados atributos nos objetos de dimensão. Você pode exibir e configurar atributos usando o Designer de Dimensão no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O painel **Atributos** da guia **Estrutura da Dimensão** do Designer de Dimensão lista os atributos que estão em uma dimensão. Use esse painel para adicionar, remover ou configurar atributos. Também é possível selecionar atributos para usar como um nível em uma nova hierarquia ou para adicionar a um nível de uma hierarquia existente.  
  
 Para exibir os atributos de uma dimensão, abra o Designer de Dimensão para a dimensão. O painel **Atributos** da guia **Estrutura da Dimensão**  do designer mostra os atributos que estão na dimensão. Você pode alternar entre uma exibição de lista, árvore ou grade, basta apontar para **Mostrar atributos em** no **dimensão** menu [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e, em seguida, clicar em um dos comandos mostrados na tabela a seguir.  
  
|Mostrar Atributos em|Description|  
|------------------------|-----------------|  
|**Lista**|Exibe os atributos no formato de lista.<br /><br /> Clique com o botão direito do mouse no atributo para excluí-lo da lista, renomeá-lo ou alterar seu uso.<br /><br /> Use esse modo de exibição para construir hierarquias. As informações do atributo e as propriedades do membro não são visíveis.|  
|**Árvore**|Exibe os atributos no formato de árvore, com a dimensão como o nó de nível superior na árvore. Use esse modo de exibição para exibir e criar propriedades do membro. Você também pode usá-lo para construir hierarquias. Expanda o atributo para exibir suas relações ou criar uma nova relação de atributo, executando um destes procedimentos:<br /><br /> Clique na dimensão, no atributo ou na propriedade do membro para exibir suas propriedades na janela **Propriedades** .<br /><br /> Clique com o botão direito do mouse no atributo ou na propriedade do membro para excluí-lo(a) da lista, renomeá-lo(a) ou alterar seu uso.|  
|**Grade**|Exibe os atributos no formato de grade. Clique em qualquer linha da grade para exibir as propriedades desse atributo.  Use esse modo de exibição para criar e configurar atributos. A grade exibe as seguintes colunas:<br /><br /> **Nome**: mostra o valor de **nome** propriedade. Digite outro nome para alterar a configuração.<br /><br /> **Uso**: Especifica se este é um atributo Regular, Key, pai ou AccountType. Clique em um valor dessa coluna selecionar uma configuração diferente.<br /><br /> **Tipo**: Especifica a categoria de business intelligence para o atributo. Clique nessa célula para selecionar uma configuração diferente.<br /><br /> **A coluna de chave**: mostra o tipo de dados OLE DB para o **KeyColumn** propriedade no atributo. Não é possível alterar essa coluna.<br /><br /> **Coluna de nome**: indica se o **NameColumn** configuração de propriedade do atributo é a mesma coluna como a configuração para o **KeyColumn** propriedade. Não é possível alterar essa coluna.|  
  
 No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], os ícones mostrados na tabela a seguir marcam os atributos de acordo com seu uso.  
  
|Ícone|Uso do atributo|  
|----------|---------------------|  
|![Ícone de atributo](../media/as-icon-attribute.gif "ícone de atributo")|Regular ou AccountType|  
|![Ícone de atributo de chave](../media/as-icon-key-attribute.gif "ícone de atributo de chave")|Chave|  
|![Ícone de atributo pai](../media/as-icon-parent-attribute.gif "ícone de atributo pai")|Pai|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)  
  
  