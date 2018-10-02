---
title: Adicionar um grupo de detalhes (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 61e5ca1b562a2b809319cf15e7fa6d5df8f6ed16
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800684"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>Adicionar um grupo de detalhes (Construtor de Relatórios e SSRS)
Em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os dados de detalhes de um conjunto de dados de relatório são especificados como um grupo sem expressão de grupo. Adicione um grupo de detalhes a uma região de dados tablix existente quando desejar exibir os dados de detalhes para uma matriz. Adicione dados de detalhes novamente que você excluiu de uma tabela ou lista ou para adicionar grupos de detalhes adicionais. Para obter mais informações sobre grupos, consulte [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Para adicionar um grupo de detalhes a uma região de dados tablix  
  
1.  Na superfície de design, clique em qualquer lugar em uma região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados selecionada.  
  
2.  No painel Agrupamento, clique com o botão direito do mouse em um grupo que seja o grupo filho mais interno. Clique em **Adicionar Grupo**e em **Grupo Filho**. A caixa de diálogo **Grupo Tablix** é aberta.  
  
3.  Em **Expressão de Grupo**, deixe a expressão em branco. Um grupo de detalhes não tem nenhuma expressão.  
  
4.  Selecione **Mostrar dados de detalhes**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Um novo grupo de detalhes é adicionado como um grupo filho ao painel Agrupamento e o identificador da linha do grupo selecionado na etapa 1 exibe o ícone do grupo de detalhes. Para obter mais informações sobre identificadores, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
