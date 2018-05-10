---
title: Adicionar um total a um grupo ou a uma região de dados Tablix (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf1b96c3-7f0f-4c94-ad08-5239c77ccfe4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a34109f5d9ffe94c6e3951fd3fa87e78c789ea00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs"></a>Adicionar um total a um grupo ou a uma região de dados Tablix (Construtor de Relatórios e SSRS)
 Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , é possível adicionar totais em uma região de dados tablix para um grupo ou para toda a região de dados. Por padrão, total é a soma dos dados numéricos, não nulos, em um grupo ou na região de dados, após a aplicação de filtros. Para adicionar totais de um grupo, clique em **Adicionar Total** no menu de atalho do grupo no painel Agrupamento. Para adicionar totais de uma célula individual na área de corpo tablix, clique em **Adicionar Total** no menu de atalho da célula. O comando **Adicionar Total** é contextual e habilitado apenas para campos numéricos. Dependendo da célula tablix selecionada, é possível adicionar um total de uma única célula selecionando uma célula na área do corpo tablix, ou de todo o grupo selecionando uma célula na área do grupo de linhas tablix ou na área do grupo de colunas tablix. Para obter mais informações sobre áreas tablix, consulte [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md).  
  
 Depois de adicionar um total, você pode alterar a função padrão Sum para outra função de agregação da lista de funções de relatório internas. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).[!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-total-for-an-individual-value-in-the-tablix-body-area"></a>Para adicionar um total de um valor individual na área do corpo tablix  
  
-   Na área do corpo da região de dados tablix, clique com o botão direito do mouse no local em que você deseja adicionar o total. A célula deve conter um campo numérico. Aponte para **Adicionar Total**e clique em **Linha** ou **Coluna**.  
  
     Uma nova linha ou coluna fora do grupo atual é adicionada à região de dados com um total padrão do campo na célula em que você clicou.  
  
     Se a região de dados tablix for uma tabela, uma linha será adicionada automaticamente.  
  
## <a name="to-add-totals-for-a-row-group"></a>Para adicionar totais de um grupo de linhas  
  
-   Na área do grupo de linhas da região de dados tablix, clique com o botão direito do mouse em uma célula para a qual você deseja adicionar totais, aponte para **Adicionar Total**e clique em **Antes** ou **Depois**.  
  
     Uma nova linha fora do grupo atual é adicionada à região de dados, e um total padrão é adicionado a todos os campos numéricos da linha.  
  
## <a name="to-add-totals-for-a-column-group"></a>Para adicionar totais de um grupo de colunas  
  
-   Na área do grupo de linhas da região de dados tablix, clique com o botão direito do mouse em uma célula da área do grupo de colunas para a qual você deseja adicionar totais, aponte para **Adicionar Total**e clique em **Antes** ou **Depois**.  
  
     Uma nova coluna fora do grupo atual é adicionada à região de dados, e um total padrão é adicionado a todos os campos numéricos da coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
