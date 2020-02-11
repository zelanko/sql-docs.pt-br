---
title: Carregar dados do MDS para o Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbe1188773d0770ff345cd54ea47e03a3c05555f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482710"
---
# <a name="load-data-from-mds-into-excel"></a>Carregar dados do MDS no Excel
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]No, você deve carregar dados do repositório do MDS para trabalhar com ele.  
  
 Se você quiser filtrar o conjunto de dados antes de carregá-lo, confira [filtro antes de carregar &#40;Suplemento MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md) em vez disso.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-load-data-from-mds-into-excel"></a>Para carregar dados do MDS no Excel  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o painel **Master Data Explorer** estiver desabilitado, isso significará que a planilha existente já contém dados gerenciados pelo MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No painel **Master Data Explorer** , na lista de entidades, clique duas vezes na entidade que você deseja carregar.  
  
    > [!NOTE]  
    >  -   Somente os primeiros um milhão de membros serão carregados no Excel. Para filtrar a lista antes de carregar na faixa de opções, no grupo **Conectar e Carregar** , clique em **Filtrar**.  
    > -   Nas colunas que são listas restritas (atributos baseados em domínio), os primeiros 25.000 valores serão carregados. Você pode alterar este número na propriedade MaximumDbaEntitySize no arquivo excelusersettings.config localizado no computador no qual o Excel está instalado. Esse arquivo está localizado em C:\Users\\<usuário\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices\\.  
  
    > [!NOTE]  
    >  Quando você carrega dados delimitados por texto usando o Suplemento para Microsoft Excel com o Excel de 32 bits, e as configurações para as propriedades **Cell Count to Load** e **Cell Count to Publish** são configuradas para o máximo de 1000, ocorrerá um erro de memória insuficiente. Você deve usar o Excel de 64 bits para usar as configurações máximas para **Contagem de Células para Carregamento** e **Contagem de Células para Publicação**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Publicar dados do Excel para o MDS &#40;Suplemento MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Carregando dados &#40;Suplemento MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Caixa de diálogo de filtro &#40;Suplemento MDS para Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [Publicando dados &#40;Suplemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
