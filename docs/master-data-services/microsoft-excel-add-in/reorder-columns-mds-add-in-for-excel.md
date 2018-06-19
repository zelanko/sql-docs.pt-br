---
title: Reordenar colunas (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e90e0e99ecf052696dc2eff7065ac1ea9ffba974
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333580"
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>Reordenar colunas (suplemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você pode reorganizar colunas filtrando a lista antes de carregar.  
  
 Quando você reorganizar atributos na caixa de diálogo **Filtro** , os dados serão carregados no Excel com a nova ordem. Porém, da próxima vez que você filtrar os dados de atributo, a ordem reverterá para a ordem no design original. Para alterar a ordem permanentemente, um administrador deverá alterar a ordem na área de **Administração do sistema** de Master Data Manager. Para obter mais informações, consulte [Change the Order of Attributes](../../master-data-services/change-the-order-of-attributes.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-reorder-mds-managed-columns"></a>Para reorganizar colunas gerenciadas por MDS  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o painel **Master Data Explorer** estiver desabilitado, isso significará que a planilha existente já contém dados gerenciados pelo MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No painel do **Master Data Explorer** , clique em uma entidade.  
  
4.  No grupo **Conectar e Carregar** , clique em **Filtrar**.  
  
5.  Na caixa de diálogo **Filtrar** , na seção **Colunas** , na lista de atributos, clique no atributo que deseja mover.  
  
6.  À direita da lista, clique na seta **Para cima** ou **Para baixo** para mover o atributo para a esquerda ou para a direita na planilha.  
  
7.  Repita a etapa 7 para cada atributo até que a ordem de cima para baixo represente a ordem da esquerda para a direita que você deseja na planilha.  
  
8.  Clique em **Carregar Dados**. A planilha será preenchida com dados gerenciados no MDS e as colunas serão exibidas na ordem que você especificou.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: Exportando dados para o Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
