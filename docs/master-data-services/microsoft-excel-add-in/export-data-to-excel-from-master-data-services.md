---
title: Exportar dados para o Excel do Master Data Services | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
caps.latest.revision: 16
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: fe35ef5b4d4d58796a4392afc3f1f3fe6c7badda
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="export-data-to-excel-from-master-data-services"></a>Exportar dados para o Excel do Master Data Services
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], é necessário exportar dados do repositório do MDS para trabalhar com eles.  
  
 Se você deseja filtrar o conjunto de dados antes de carregá-lo, consulte [Filtrar dados antes da exportação &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-export-data-from-mds-into-excel"></a>Para exportar dados do MDS no Excel  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o painel **Master Data Explorer** estiver desabilitado, isso significará que a planilha existente já contém dados gerenciados pelo MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No painel **Master Data Explorer** , na lista de entidades, clique duas vezes na entidade que você deseja carregar.  
  
    > [!NOTE]  
    >  -   Somente os primeiros um milhão de membros serão carregados no Excel. Para filtrar a lista antes de carregar na faixa de opções, no grupo **Conectar e Carregar** , clique em **Filtrar**.  
    > -   Nas colunas que são listas restritas (atributos baseados em domínio), por padrão, somente os primeiros 25.000 valores serão carregados. Você pode alterar este número na propriedade MaximumDbaEntitySize no arquivo excelusersettings.config localizado no computador no qual o Excel está instalado. Este arquivo está localizado em C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server\130\MasterDataServices\\.  
    >   
    >      Se um atributo baseado em domínio tiver um número de valores que ultrapassa a configuração da propriedade MaximumDbEntitySize, a lista de valores não será carregada.  
  
    > [!NOTE]  
    >  Quando você carrega dados delimitados por texto usando o Suplemento para Microsoft Excel com o Excel de 32 bits, e as configurações para as propriedades **Cell Count to Load** e **Cell Count to Publish** são configuradas para o máximo de 1000, ocorrerá um erro de memória insuficiente. Você deve usar o Excel de 64 bits para usar as configurações máximas para **Contagem de Células para Carregamento** e **Contagem de Células para Publicação**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Importar dados do Excel para o Master Data Services &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral: Exportando dados para o Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Caixa de diálogo Filtrar &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
