---
title: Adicionar, alterar ou excluir um parâmetro de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eb0d29f62a3751f0b8b6acd1c33c7b7f7eb10ff2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582066"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>Adicionar, alterar ou excluir um parâmetro de relatório (Construtor de Relatórios e SSRS)
  Um parâmetro de relatório fornece uma maneira de escolher dados de relatório, conectar relatórios relacionados e variar a apresentação do relatório. Você pode fornecer um valor padrão e uma lista de valores disponíveis e o usuário pode alterar a seleção.  
  
 Depois de publicar um relatório, você poderá alterar os valores padrão, os valores disponíveis e outras propriedades para um parâmetro de relatório no servidor de relatórios. Você pode fornecer vários conjuntos de valores de parâmetros padrão criando relatórios vinculados. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Este artigo é sobre como adicionar parâmetros de relatório em um relatório paginado no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ou no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Você também pode adicionar parâmetros de relatório em relatórios móveis no  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]. Consulte [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) para obter mais informações.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>Para adicionar ou editar um parâmetro de relatório  
  
1.  No [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ou no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no painel **Dados de Relatório** , clique com o botão direito do mouse no nó **Parâmetros** e clique em **Adicionar Parâmetro**. A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
2.  Em **Nome**, digite o nome do parâmetro ou aceite o nome padrão.  
  
3.  No **Prompt**, digite o texto que é exibido ao lado da caixa de texto do parâmetro quando o usuário executa o relatório.  
  
4.  Na lista **Tipo de dados**, selecione o tipo de dados do valor do parâmetro.  
  
5.  Se o parâmetro pode conter um valor em branco, selecione **Permitir valor em branco**.  
  
6.  Se o parâmetro pode conter um valor nulo, selecione **Permitir valor nulo**.  
  
7.  Para permitir que um usuário selecione mais de um valor do parâmetro, selecione **Permitir diversos valores**.  
  
8.  Defina a opção de visibilidade.  
  
    -   Para mostrar o parâmetro na barra de ferramentas na parte superior do relatório, selecione **Visível**.  
  
    -   Para ocultar o parâmetro para que ele não seja exibido na barra de ferramentas, selecione **Oculto**.  
  
    -   Para ocultar o parâmetro e impedi-lo de ser modificado no servidor de relatórios depois que o relatório é publicado, selecione **Interno**. O parâmetro de relatório só pode ser exibido na definição do relatório. Para essa opção, você deve definir um valor padrão ou permitir que o parâmetro aceite um valor nulo.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>Para excluir um parâmetro de relatório  
  
1.  No painel **Dados do Relatório** , expanda o nó **Parâmetros** .  
  
2.  Clique com o botão direito do mouse no parâmetro do relatório e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar, alterar ou excluir valores disponíveis para um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [Adicionar, alterar ou excluir valores padrão de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Referências de coleção de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Adicionar um parâmetro com vários valores a um relatório](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
