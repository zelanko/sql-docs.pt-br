---
title: Exibir atributos no designer de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb12bd6499796ff7f2cfb09ccd4c176914c8117
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175795"
---
# <a name="view-attributes-in-dimension-designer"></a>Exibir atributos no Designer de Dimensão
  São criados atributos nos objetos de dimensão. Você pode exibir e configurar atributos usando o designer de dimensão [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]no. O painel **Atributos** da guia **Estrutura da Dimensão** do Designer de Dimensão lista os atributos que estão em uma dimensão. Use esse painel para adicionar, remover ou configurar atributos. Também é possível selecionar atributos para usar como um nível em uma nova hierarquia ou para adicionar a um nível de uma hierarquia existente.

 Para exibir os atributos de uma dimensão, abra o Designer de Dimensão para a dimensão. O painel **Atributos** da guia **Estrutura da Dimensão**  do designer mostra os atributos que estão na dimensão. Você pode alternar entre uma exibição de lista, árvore ou grade apontando para **Mostrar atributos no** no menu **dimensão** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e clicando em um dos comandos mostrados na tabela a seguir.

|Mostrar Atributos em|Descrição|
|------------------------|-----------------|
|**Lista**|Exibe os atributos no formato de lista.<br /><br /> Clique com o botão direito do mouse no atributo para excluí-lo da lista, renomeá-lo ou alterar seu uso.<br /><br /> Use esse modo de exibição para construir hierarquias. As informações do atributo e as propriedades do membro não são visíveis.|
|**Três**|Exibe os atributos no formato de árvore, com a dimensão como o nó de nível superior na árvore. Use esse modo de exibição para exibir e criar propriedades do membro. Você também pode usá-lo para construir hierarquias. Expanda o atributo para exibir suas relações ou criar uma nova relação de atributo, executando um destes procedimentos:<br /><br /> Clique na dimensão, no atributo ou na propriedade do membro para exibir suas propriedades na janela **Propriedades** .<br /><br /> Clique com o botão direito do mouse no atributo ou na propriedade do membro para excluí-lo(a) da lista, renomeá-lo(a) ou alterar seu uso.|
|**Grade**|Exibe os atributos no formato de grade. Clique em qualquer linha da grade para exibir as propriedades desse atributo.  Use esse modo de exibição para criar e configurar atributos. A grade exibe as seguintes colunas:<br /><br /> **Nome**: mostra o valor da propriedade **Name** . Digite outro nome para alterar a configuração.<br /><br /> **Uso**: especifica se este é um atributo regular, Key, Parent ou AccountType. Clique em um valor dessa coluna selecionar uma configuração diferente.<br /><br /> **Tipo**: especifica a categoria de Business Intelligence para o atributo. Clique nessa célula para selecionar uma configuração diferente.<br /><br /> **Coluna de chave**: mostra o tipo de dados OLE DB para a propriedade **KeyColumn** no atributo. Não é possível alterar essa coluna.<br /><br /> **Coluna de nome**: indica se a configuração da propriedade **NameColumn** no atributo é a mesma coluna que a configuração da propriedade **KeyColumn** . Não é possível alterar essa coluna.|

 No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], os ícones mostrados na tabela a seguir marcam os atributos de acordo com seu uso.

|ícone|Uso do atributo|
|----------|---------------------|
|![Ícone de atributo](../media/as-icon-attribute.gif "Ícone de atributo")|Regular ou AccountType|
|![Ícone de atributo de chave](../media/as-icon-key-attribute.gif "Ícone de atributo de chave")|Chave|
|![Ícone de atributo pai](../media/as-icon-parent-attribute.gif "Ícone de atributo pai")|Pai|

## <a name="see-also"></a>Consulte Também
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)


