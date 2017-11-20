---
title: "Filtrar dados antes da exportação (Suplemento MDS para Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 13a0720defc0a9e837f771a73f44bca343773ce1
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="filter-data-before-exporting-mds-add-in-for-excel"></a>Filtrar dados antes da exportação (Suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], filtre os dados quando quiser limitar o tamanho ou o escopo dos dados que estiver exportando no Excel.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-filter-data-before-exporting"></a>Para filtrar dados antes de exportar  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o painel **Master Data Explorer** estiver desabilitado, isso significará que a planilha existente já contém dados gerenciados pelo MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No painel do **Master Data Explorer** , na lista de entidades, clique na entidade que você deseja filtrar.  
  
4.  Na faixa de opções, no grupo **Conectar e Carregar** , clique em **Filtrar**.  
  
5.  Preencha a caixa de diálogo **Filtrar** selecionando os atributos (colunas) a serem exibidos, definindo a ordem das colunas e, se necessário, filtrando os dados para que menos linhas sejam retornadas. Abra o painel **Resumo** para saber a quantidade de dados que será retornada. Para obter mais informações, consulte [Caixa de diálogo Filtrar &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md).  
  
6.  Clique em **Carregar Dados**. A planilha será preenchida com os dados gerenciados no MDS.  
  
    > [!NOTE]  
    >  -   Somente os primeiros um milhão de membros serão carregados no Excel.  
    > -   Nas colunas que são listas restritas (atributos baseados em domínio), por padrão, somente os primeiros 25000 valores serão carregados.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Importar dados do Excel para o Master Data Services &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral: Exportando dados para o Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Caixa de diálogo Filtrar &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [Reordenar colunas &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  

