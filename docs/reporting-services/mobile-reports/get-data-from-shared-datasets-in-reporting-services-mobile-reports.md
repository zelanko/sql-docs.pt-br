---
title: Obter dados de conjuntos de dados compartilhados em relatórios móveis do Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cac1a32b49fde5b41c0a8ef21706d873ce037cd3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63061108"
---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Obter dados de conjuntos de dados compartilhados nos relatórios móveis do Reporting Services
Além do [carregamento de dados de arquivos do Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md), o Publicador de Relatórios Móveis do Microsoft SQL Server também pode acessar dados de praticamente qualquer origem. O acesso aos dados exige uma fonte de dados compartilhada, configurada em um portal da Web do Reporting Services. Leia mais sobre como [criar fontes de dados compartilhadas](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) e [criar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md).  
  
Depois que as fontes de dados e os conjuntos de dados compartilhados forem configurados no servidor do Reporting Services, você poderá usá-los nos relatórios móveis criados no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Depois de se conectar a um servidor [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] por meio do [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], conectar um relatório móvel a um conjunto de dados compartilhado é simples.   
  
1. Na guia **Dados** , selecione **Adicionar Dados**.  
  
2. Selecione **Servidor de Relatórios**.   
  
3.  Se esta for a primeira vez que você se conecta ao servidor, preencha o nome do servidor e seu nome e senha. Coloque o nome do servidor na caixa de endereço do servidor neste formato:  
  
    \<"servername">/reports/  
  
    Como neste exemplo:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. Quando você seleciona o servidor [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , vê os conjuntos de dados disponíveis nas pastas. Selecione um conjunto de dados para importar os dados para [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
Depois de importar o conjunto de dados, você pode criar seu relatório móvel como faria com dados simulados ou dados locais de um arquivo Excel.  
  
Por padrão, o conjunto de dados compartilhado é sempre atualizado com os dados mais recentes, porque sempre que alguém exibe um relatório móvel com base no conjunto de dados, o SQL Server executa a consulta subjacente e retorna os dados mais recentes. Obviamente, se muitas pessoas exibirem seu relatório móvel isso pode não ser o ideal, assim você pode definir o cache para executar a consulta periodicamente e armazenar em cache o conjunto de dados resultante. Esta postagem de blog explica [como cache e atualização de dados funcionam no portal da Web](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/).  
  
## <a name="add-edit-or-remove-a-report-server"></a>Adicionar, editar ou remover um servidor de relatório  
  
Se você já estiver se conectado a um servidor de relatório, quando você selecionar **Adicionar dados** na guia Dados, você não verá uma opção para adicionar outro servidor de relatório. Em vez disso, siga estas etapas.  
  
1. No canto superior esquerdo, selecione **Conexões**.  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   O painel Conexão do servidor é aberto do lado direito.  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. Adicione uma nova conexão de servidor, editar ou remova conexões existentes.  
  
### <a name="see-also"></a>Confira também  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Portal da Web (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo de iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo do iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  

