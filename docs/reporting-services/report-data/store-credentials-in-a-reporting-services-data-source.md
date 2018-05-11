---
title: Armazenar credenciais em uma fonte de dados do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: fa7bc5471455e428fb680dbe0369bc1fd4888dbe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Store Credentials in a Reporting Services Data Source
  Você pode configurar credenciais armazenadas usadas por um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para acessar dados externos de um relatório. As credenciais armazenadas serão usadas se o relatório for executado autônomo, por exemplo, uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que publica um relatório como um email. O servidor de relatórios recupera e usa as credenciais quando o processamento do relatório é agendado ou disparado. Este tópico explica como configurar credenciais armazenadas para servidores de relatórios tanto no modo nativo quanto no modo do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint|  
  
-   [Configurar credenciais armazenadas para uma fonte de dados específica do relatório (modo nativo)](#bkmk_stored_credentials_data_source_native)  
  
-   [Configurar credenciais armazenadas para uma fonte de dados específica do relatório (modo SharePoint)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [Configurar credenciais armazenadas para uma fonte de dados compartilhada (modo nativo)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [Configurar credenciais armazenadas para uma fonte de dados compartilhada (modo SharePoint)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> Requisitos da política de segurança para credenciais armazenadas  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") é necessário que a conta usada para as credenciais armazenadas esteja configurada para uma das políticas de segurança a seguir no servidor de relatório. É recomendável escolher a política com o nível mínimo de permissões que você precisa para o ambiente.  
  
1.  **Permitir logon localmente**. Para obter mais informações, consulte [Permitir logon localmente](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Fazer logon como um trabalho em lotes**. Para obter mais informações, consulte [Fazer logon como um trabalho em lotes](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Para obter informações gerais sobre as políticas, consulte [Editar configurações de segurança em um objeto de política de grupo](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Configurar credenciais armazenadas para uma fonte de dados específica do relatório (modo nativo)  
  
1.  No Gerenciador de Relatórios no modo nativo, navegue até a pasta que contém o relatório. Clique no menu de contexto do item ![menu de contexto no Gerenciador de Relatórios para itens do SSRS](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "menu de contexto no Gerenciador de Relatórios para itens do SSRS").  
  
2.  Clique em **Gerenciar** e clique em **Fontes de Dados**.  
  
3.  Selecione **Uma fonte de dados personalizada**.  
  
4.  Na lista **Tipo de Fonte de Dados** , selecione a extensão de processamento de dados usada para processar os dados da fonte de dados.  
  
5.  Em **Cadeia de Conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Para **Conectar usando**, selecione **Credenciais armazenadas com segurança no servidor de relatório**.  
  
7.  Digite um nome de usuário e uma senha.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a neste formato: \<domain>\\<account\>. Em seguida, selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados.**  
  
    -   Se o nome de usuário e a senha forem credenciais do banco de dados, não selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o servidor do banco de dados oferecer suporte a representação ou delegação, é possível selecionar **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados**.  
  
8.  Clique em **Aplicar**.  
  
     ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Requisitos da política de segurança para credenciais armazenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Configurar credenciais armazenadas para uma fonte de dados específica do relatório (modo SharePoint)  
  
1.  Navegue para a biblioteca de documentos que contém o relatório e, em seguida, clique em Abrir Menu ![menu de contexto da biblioteca de documentos para itens do SSRS](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu de contexto da biblioteca de documentos para itens do SSRS").  
  
2.  Clique no segundo Abrir Menu ![menu de contexto da biblioteca de documentos para itens do SSRS](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu de contexto da biblioteca de documentos para itens do SSRS") e, em seguida, clique em **Gerenciar Fontes de Dados**.  
  
3.  Clique no nome da fonte de dados **Personalizado** que deseja configurar com as credenciais armazenadas.  
  
4.  Na lista **Tipo de Fonte de Dados** , selecione a extensão de processamento de dados usada para processar os dados da fonte de dados.  
  
5.  Em **Cadeia de Conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Em **Credenciais**, selecione **Credenciais Armazenadas**.  
  
7.  Digite um **nome de usuário** e uma **senha**.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a neste formato: \<domain>\\<account\>. Em seguida, selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados.**  
  
    -   Se o nome de usuário e a senha forem credenciais de banco de dados, não selecione **Usar como credenciais do Windows**. Se o servidor de banco de dados oferecer suporte à representação ou delegação, você poderá selecionar **Definir o contexto de execução para esta conta**.  
  
8.  Clique em **OK**.  
  
     ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Requisitos da política de segurança para credenciais armazenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Configurar credenciais armazenadas para uma fonte de dados compartilhada (modo nativo)  
  
1.  No Gerenciador de Relatórios no modo nativo, navegue até o item da fonte de dados compartilhada. ![Ícone Fonte de dados compartilhada](../../reporting-services/report-data/media/hlp-16datasource.png "Ícone Fonte de dados compartilhada")  
  
2.  Clique no menu de contexto ![menu de contexto no Gerenciador de Relatórios para itens do SSRS](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "menu de contexto no Gerenciador de Relatórios para itens do SSRS") e, em seguida, clique em **Gerenciar**.  
  
3.  Na lista **Tipo de Fonte de Dados** , especifique a extensão de processamento de dados usada para processar dados da fonte de dados.  
  
4.  Em **Cadeia de Conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda não especificar credenciais na cadeia de conexão.  
  
     O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Digite um nome de usuário e uma senha.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a neste formato: \<domain>\\<account\>. Em seguida, selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados.**  
  
    -   Se o nome de usuário e a senha forem credenciais do banco de dados, não selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o servidor do banco de dados oferecer suporte a representação ou delegação, é possível selecionar **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados**.  
  
6.  Clique em **Aplicar**.  
  
     ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Requisitos da política de segurança para credenciais armazenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Configurar credenciais armazenadas para uma fonte de dados compartilhada (modo SharePoint)  
  
1.  Na biblioteca de documentos, navegue para o item de fonte de dados compartilhada. ![Ícone de fonte de dados compartilhada](../../reporting-services/report-data/media/hlp-16datasource.png "Ícone de fonte de dados compartilhada")  
  
2.  Clique no menu de contexto ![menu de contexto da biblioteca de documentos para itens do SSRS](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu de contexto da biblioteca de documentos para itens do SSRS") e, em seguida, clique no segundo menu de contexto ![menu de contexto da biblioteca de documentos para itens do SSRS](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu de contexto da biblioteca de documentos para itens do SSRS").  
  
3.  Clique em **Editar Definição da Fonte de Dados**.  
  
4.  Na lista **Tipo de Fonte de Dados** , especifique a extensão de processamento de dados usada para processar dados da fonte de dados.  
  
5.  Em **Cadeia de Conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda não especificar credenciais na cadeia de conexão.  
  
     O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Digite um nome de usuário e uma senha.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a no formato \<domain>\\<account\> e, em seguida, selecione **Usar as credenciais do Windows.**  
  
    -   Se o nome de usuário e a senha forem credenciais de banco de dados, não selecione **Usar como credenciais do Windows**. Se o servidor de banco de dados oferecer suporte à representação ou delegação, você poderá selecionar **Definir o contexto de execução para esta conta**.  
  
7.  Clique em **OK**.  
  
     ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Requisitos da política de segurança para credenciais armazenadas](#bkmk_top)  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Configurar as propriedades de fonte de dados de um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Página de propriedades Fontes de Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)   
 [Página Nova Fonte de Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/35563d4c-a3d5-4f95-bf46-605da9dfcbb8)  
  
  
