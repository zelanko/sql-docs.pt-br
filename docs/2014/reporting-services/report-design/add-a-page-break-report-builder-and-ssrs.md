---
title: Adicionar uma quebra de página (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0ff44ce1f100f6845999f038d21f14efce9a5654
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053446"
---
# <a name="add-a-page-break-report-builder-and-ssrs"></a>Adicionar uma quebra de página (Construtor de Relatórios e SSRS)
  É possível adicionar uma quebra de página a retângulos, regiões de dados ou grupos dentro das regiões de dados para controlar a quantidade de informações em cada página. A adição de quebras de página pode melhorar o desempenho de relatórios publicados porque apenas os itens em cada página precisam ser processados conforme o relatório é exibido. Quando todo o relatório ocupa uma única página, todos os itens devem ser processados antes de o relatório ser exibido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-break-to-a-data-region"></a>Para adicionar uma quebra de página a uma região de dados  
  
1.  Na superfície de design, clique com o botão direito do mouse na alça de canto da região de dados e clique em **Propriedades do Tablix**.  
  
2.  Na guia **Geral** , em **Opções de quebra de página**, selecione uma das seguintes opções:  
  
    -   **Adicionar uma quebra de página antes**. Selecione essa opção para adicionar uma quebra de página antes da tabela.  
  
    -   **Adicionar uma quebra de página após**. Selecione essa opção para adicionar uma quebra de página após a tabela.  
  
    -   **Ajustar a tabela em uma página, se possível**. Selecione essa opção para que os dados permaneçam em uma única página.  
  
### <a name="to-add-a-page-break-to-a-rectangle"></a>Para adicionar uma quebra de página a um retângulo  
  
1.  Na superfície de design, clique com o botão direito do mouse no retângulo em que quer adicionar uma quebra de página e clique em **Propriedades do Retângulo**.  
  
2.  Na guia **Geral** , em **Opções de quebra de página**, selecione uma das seguintes opções:  
  
    -   **Adicionar uma quebra de página antes**. Selecione essa opção para adicionar uma quebra de página antes do retângulo.  
  
    -   **Adicionar uma quebra de página após**. Selecione essa opção para adicionar uma quebra de página após o retângulo.  
  
    -   **Omitir borda na quebra de página**. Selecione essa opção quando não desejar uma borda na quebra de página.  
  
    -   **Manter o conteúdo em uma única página, se possível**. Selecione essa opção quando desejar que o conteúdo dentro do retângulo permaneça em uma única página.  
  
### <a name="to-add-a-page-break-to-a-row-group-in-a-table-matrix-or-list"></a>Para adicionar uma quebra de página a um grupo de linhas de uma tabela, matriz ou lista  
  
1.  No painel Agrupamento, clique com o botão direito do mouse no grupo de linhas e clique em **Propriedades do Grupo**.  
  
    > [!NOTE]  
    >  Quebras de página em grupos de colunas são ignoradas.  
  
2.  Na guia **Quebras de Página** , selecione **Entre cada instância de um grupo** para adicionar uma quebra de página entre cada instância de um grupo na tabela.  
  
3.  Opcionalmente, selecione **Também no início de um grupo** ou **Também no fim de um grupo** para especificar que uma quebra de página seja adicionada quando um grupo for iniciado ou finalizado na tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [Cabeçalhos e rodapés de página &#40;relatórios e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)  
  
  
