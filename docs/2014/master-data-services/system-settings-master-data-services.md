---
title: Configurações do sistema (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Master Data Services, system settings
- system settings [Master Data Services]
ms.assetid: 83075cdf-f059-4646-8ba2-19be8202f130
caps.latest.revision: 13
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9ab93ff71c31ad9606b6137fea051bb73cfe24c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310096"
---
# <a name="system-settings-master-data-services"></a>Configurações do sistema (Master Data Services)
  Para todos os aplicativos Web e serviços Web associados a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , você pode definir configurações do sistema.  
  
 Muitas dessas configurações podem ser ajustadas no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] , na página **Banco de Dados** . Outras podem ser ajustadas na tabela de Configurações do Sistema (mdm.tblSystemSetting) no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 As configurações podem ser agrupadas nas seguintes categorias:  
  
-   [Configurações gerais](#General)  
  
-   [Configurações de gerenciamento de versão](#Versions)  
  
-   [Configurações de preparação](#Staging)  
  
-   [Configurações do Gerenciador](#Explorer)  
  
-   [Configurações de Suplemento para Excel](#xls)  
  
-   [Configurações de regra de negócio](#BusinessRules)  
  
-   [Configurações de notificação](#Notifications)  
  
-   [Configurações de segurança](#Security)  
  
-   [Não usado](#NotUsed)  
  
##  <a name="General"></a> Configurações gerais  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**Tempo limite da conexão de banco de dados**|**DatabaseConnectionTimeOut**|O número de segundos permitido pelo banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para que uma conexão seja concluída. Se a conexão não for concluída dentro desse período, ela será cancelada e um erro será retornado. O valor padrão é **60** segundos (1 minuto).|  
|**Tempo limite do comando de banco de dados**|**DatabaseCommandTimeOut**|O número de segundos permitido pelo banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para que um comando seja concluído. Se o comando não for concluído dentro desse período, ele será cancelado e um erro será retornado. O valor padrão é **3600** segundos (60 minutos).|  
|**Tempo limite do serviço Web**|**ServerTimeOut**|O número de segundos permitido pelo ASP.NET para que uma solicitação de página do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] seja concluída. Se a solicitação não concluir dentro desse período, ela será cancelada e um erro será retornado. O valor padrão é **120000** segundos (2.000 minutos).|  
|**Tempo limite de cliente**|**ClientTimeOut**|O número de segundos de inatividade antes de o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] retornar à página inicial. O valor padrão é **300** segundos (5 minutos).|  
|**Número de linhas por lote**|**RowsPerBatch**|O número de registros a serem recuperados em cada lote pelo serviço Web. O valor padrão é **50**.|  
||**ApplicationName**|O texto que é exibido em logs de eventos. O valor padrão é **MDM**.|  
||**SiteTitle**|O texto que é exibido na barra de título do navegador da Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O valor padrão é **Master Data Manager**.|  
  
##  <a name="Versions"></a> Configurações de gerenciamento de versão  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**Copiar somente as versões confirmadas**|**CopyOnlyCommittedVersion**|No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], determina se os usuários podem copiar versões de modelos com um status **Confirmado**ou versões com qualquer status. O valor padrão é **Yes** ou **1**, indicando que os usuários podem copiar somente versões com status **Confirmado** . Altere para **No** ou **2** para permitir que os usuários copiem todas as versões.|  
  
 Para obter mais informações, consulte [Versões &#40;Master Data Services&#41;](versions-master-data-services.md).  
  
##  <a name="Staging"></a> Configurações de preparação  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**Registrar em log todas as transações de preparação**|**StagingTransactionLogging**|Aplica-se somente ao SQL Server 2008 R2. Determina se as transações serão registradas em log quando os registros de preparação forem carregados no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . O valor padrão é **Off** or **2**. Altere para **On** ou **1** para ativar o registro em log.|  
|**Intervalo do lote de preparação**|**StagingBatchInterval**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , o número de segundos depois que você seleciona **Iniciar Lotes** para que seu lote seja processado. O valor padrão é **60** segundos (1 minuto).|  
  
 Para obter mais informações, consulte [Importação de dados &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
##  <a name="Explorer"></a> Configurações do Gerenciador  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**Número de membros na hierarquia por padrão**|**HierarchyChildNodeLimit**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , o número máximo de membros exibidos em cada nó de hierarquia antes que **...mais...** seja exibido. Você pode clicar em **...mais...** para mostrar o próximo grupo de membros. O valor padrão é **50**.|  
|**Mostrar nomes na hierarquia por padrão**|**ShowNamesInHierarchy**|Na área funcional do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , determina a configuração padrão que é selecionada quando você exibe hierarquias.<br /><br /> O valor padrão é **Yes** ou **1**, indicando que são exibidos o nome e o código de cada membro. Altere para **No** ou **2** para exibir somente o código.|  
|**Número de atributos baseados em domínio em lista**|**DBAListRowLimit**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **Explorer** functional area, the number of attributes that are displayed in a list when you double-click a domain-based attribute value in the grid. O valor padrão é **50**. Se existirem mais de 50 membros, uma caixa de diálogo pesquisável será exibida no lugar.|  
||**GridFilterDefaultFuzzySimilarityLevel**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , o nível de similaridade usado ao empregar os critérios de filtragem **Correspondências** . O valor padrão é **0.3**. Defina um valor próximo de **1** para retornar uma correspondência mais próxima dos critérios de pesquisa. Defina como **1** para obter uma correspondência exata.|  
  
##  <a name="xls"></a> Configurações de Suplemento para Excel  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|Mostrar Suplemento para texto do Excel na página inicial do site|ShowAddInText|Na página inicial do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , mostre um link para usuários baixarem o [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|  
|Caminho de instalação do Suplemento para Excel na página inicial do site|AddInURL|Na página inicial do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , se o link para o [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] for exibido, o local para onde os usuários se dirigem quando clicam no link.|  
  
##  <a name="BusinessRules"></a> Configurações de regra de negócio  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**Número usado para incrementar novas regras de negócio**|**BusinessRuleDefaultPriorityIncrement**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , o número pelo qual a prioridade de cada nova regra de negócio é incrementada. O valor padrão é **10**.|  
|**Número de membros para os quais aplicar as regras de negócio**|**BusinessRuleRealtimeMemberCount**|Na área funcional do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , o número máximo de membros na grade aos quais as regras de negócio serão aplicadas. No [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)], o número máximo de membros na planilha ativa aos quais as regras de negócio serão aplicadas. O valor padrão é **10000**.|  
  
 Para obter mais informações, consulte [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md).  
  
##  <a name="Notifications"></a> Configurações de notificação  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
|**URL do Master Data Manager para notificações**|**MDMRootURL**|A URL do aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], que é usada no link em notificações por email; por exemplo, http://constoso/mds.|  
|**Intervalo de emails de notificação**|**NotificationInterval**|A frequência, em segundos, de envio de emails de notificação. O valor padrão é **120** segundos (2 minutos).|  
|**Número de notificações em um único email**|**NotificationsPerEmail**|O número máximo de problemas de validação que serão listados em um único email de notificação. Problemas adicionais, caso existam, não serão incluídos no email, mas estarão disponíveis no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].|  
|**Formato de email padrão**|**EmailFormat**|O formato de todas as notificações por email. O valor padrão é **HTML** or **1**. A configuração de banco de dados **2** indica **Texto**.<br /><br /> Observação: você pode substituir isso por um usuário individual no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], alterando e salvando o **Formato de email** na guia **Geral** do usuário.|  
|**Expressão regular para endereço de email**|**EmailRegExPattern**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , a expressão regular usada para validar o endereço de email inserido na guia **Geral** do usuário. Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](http://go.microsoft.com/fwlink/?LinkId=164401) na biblioteca do MSDN.|  
|**Conta do Database Mail**|**EmailProfilePrincipalAccount**|Exibe a conta do Database Mail a ser usada ao enviar notificações por email. O perfil padrão é **mds_email_user**.|  
|**Perfil do Database Mail**|**DatabaseMailProfile**|O perfil do Database Mail a ser usado ao enviar notificações por email. O valor padrão é vazio.|  
||**ValidationIssueHTML**|No formato HTML, o texto do email que os usuários obtêm quando há falha na validação de uma regra de negócios.|  
||**ValidationIssueText**|No formato de texto simples, o texto do email que os usuários obtêm quando há falha na validação de uma regra de negócios.|  
||**VersionStatusChangeText**|O texto sem-formatação, o texto do email que os usuários obtêm quando muda o status de uma versão. Apenas os usuários com permissão para **Atualizar** o modelo inteiro recebem este email.|  
||**VersionStatusChangeHTML**|No formato HTML, o texto do email que os usuários obtêm quando muda o status de uma versão. Apenas os usuários com permissão para **Atualizar** o modelo inteiro recebem este email.|  
  
 Para obter mais informações, consulte [Notificações &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md).  
  
##  <a name="Security"></a> Configurações de segurança  
  
|Configuração do Gerenciador de Configuração|Configuração do sistema|Description|  
|-----------------------------------|--------------------|-----------------|  
||**SecurityMemberProcessInterval**|Na área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **do** , a frequência, em segundos, com que as permissões de usuário e grupo definidas na guia **Membros da Hierarquia** são aplicadas. O valor padrão é **3600** segundos (60 minutos).|  
  
 Para obter mais informações, consulte [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
##  <a name="NotUsed"></a> Não usado  
 As configurações a seguir da tabela de Configurações de Sistema não são usadas.  
  
-   **SecurityMode**  
  
-   **MDSHubName**  
  
-   **ApplicationLogging**  
  
-   **ReportServer**  
  
-   **ReportDirectory**  
  
-   **BusinessRuleEngineIterationLimit**  
  
-   **BusinessRuleExtensibility**  
  
-   **AttributeExplorerMarkAllActionMemberCount**  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de objeto de banco de dados &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
