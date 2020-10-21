---
title: Tarefas de instalação
description: Este artigo fornece uma visão geral da instalação do Master Data Services, incluindo tarefas de instalação e pré-instalação e pós-instalação.
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 00248c7767e3b6205d19c395a1556ca8693e798e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92257838"
---
# <a name="installation-tasks-for-master-data-services"></a>Tarefas de instalação do Master Data Services

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo fornece uma visão geral das tarefas de instalação, com links para instruções. Para obter instruções de instalação e configuração do Master Data Services, consulte [Configuração e instalação do Master Data Services](../../master-data-services/master-data-services-installation-and-configuration.md) 
  
-   [Tarefas pré-instalação](#preinstall): verificar os requisitos do sistema antes da instalação do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
-   [Operações de Instalação](#install): instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o prompt de comando.  
  
-   [Tarefas pós-instalação](#postinstall): abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para concluir operações pós-instalação. Criar e configurar o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web, e implantar um modelo de exemplo.  
  
##  <a name="pre-installation-tasks"></a><a name="preinstall"></a> Tarefas de pré-instalação  
  
|Ação|Detalhes|Tópicos Relacionados|  
|------------|-------------|--------------------|  
|Verificar os requisitos de instalação|O computador onde a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada deve atender aos requisitos mínimos de:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalação.<br /><br /> O Aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web.<br /><br /> O banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , se for hospedado no mesmo computador do aplicativo Web.<br /><br /> <br /><br /> Você pode separar o computador do servidor Web e o computador do servidor de banco de dados executando a Instalação somente no computador do servidor Web e criando o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador remoto que execute uma versão e edição com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Recursos com suporte das edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)<br /><br /> [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Requisitos do aplicativo Web &#40;Master Data Service&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)<br /><br /> [Requisitos do banco de dados &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)|  
|Configurar as funções, serviços de função e recursos necessários|Antes de executar a Instalação, configure o computador com as funções, serviços de função e recursos necessários do Windows.<br /><br /> Observação: embora esta etapa possa ser executada posteriormente no fluxo de trabalho, é útil configurar isso antes de executar a Instalação para que você possa executar as tarefas de configuração da Web imediatamente após a instalação.|[Requisitos do aplicativo Web &#40;Master Data Service&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)|  
|Revisar as considerações de suporte a idioma|Determine o idioma em que deseja instalar e executar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Implantações multilíngues e globais &#40;Master Data Services&#41;](../../master-data-services/install-windows/multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="installation-operations"></a><a name="install"></a> Operações de Instalação  
  
|Ação|Detalhes|Tópicos Relacionados|  
|------------|-------------|--------------------|  
|Execute a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|No computador que hospedará o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , use a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um prompt de comando para instalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Ao usar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponível na página **Seleção de Recursos** , em **Recursos Compartilhados**. Ao usar um prompt de comando, o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponível como um parâmetro de recurso. Observe que o processo de instalação de linha de comando instala o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], mas não o configura. Você deve configurá-lo usando o Gerenciador de Configurações do Master Data Services.<br /><br /> O processo de instalação:<br /><br /> Instala as pastas e arquivos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no local especificado para recursos compartilhados e atribui permissões a esses objetos.<br /><br /> Registra os assemblies do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no GAC (Cache de Assembly Global).<br /><br /> Instala [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].|[Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="post-installation-tasks"></a><a name="postinstall"></a> Tarefas pós-instalação  
  
|Ação|Detalhes|Tópicos Relacionados|  
|------------|-------------|--------------------|  
|Abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para concluir operações pós-instalação.|Após a conclusão da instalação, abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] executa as seguintes operações de pós-instalação no computador local:<br /><br /> Cria um grupo do Windows, **MDS_ServiceAccounts**, para conter contas de serviço do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para pools de aplicativos.<br /><br /> No caminho de instalação do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , cria a pasta MDSTempDir e atribui permissões para **MDS_ServiceAccounts**. É nessa pasta que são compilados arquivos de compilação temporários para o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] arquivo Web.config, configura o atributo **tempDirectory** do **\<compilation>** elemento com o caminho para a pasta MDSTempDir.|[Permissões de pasta e arquivo &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)<br /><br /> [Referência de configuração da Web &#40;Master Data Services&#41;](../../master-data-services/web-configuration-reference-master-data-services.md)|  
|Criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para seus dados mestres.|[Criar um banco de dados do Master Data Services](../../master-data-services/install-windows/create-a-master-data-services-database.md)|  
|Criar um aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar e configurar um aplicativo Web que hospedará o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|[Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)|  
|Associar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a um aplicativo Web|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para associar o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ao banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Associar um banco de dados do Master Data Services a um aplicativo Web](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)|  
|Configurar a segurança aprimorada do Internet Explorer|Quando você instala o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador com Windows Server 2012, talvez seja necessário configurar a Segurança Avançada do Internet Explorer para permitir script para o site do aplicativo do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Caso contrário, haverá falha ao navegar até o site de aplicativo do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] no computador de servidor.|[Internet Explorer: configuração de segurança aprimorada](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10))|  
|Instalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|Os usuários que trabalharão com dados mestre podem instalar o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)].|[https://go.microsoft.com/fwlink/?LinkID=398159](https://go.microsoft.com/fwlink/?LinkID=398159)|  
|Habilitar a integração do DQS (Data Quality Services)|Para usuários do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], habilite a integração com o recurso DQS que pode ser usado para fazer a correspondência de dados semelhantes.|[Habilitar a integração do Data Quality Services com Master Data Services](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)|  
|Implantar um modelo de exemplo|Pacotes de modelo de exemplo são instalados com o Master Data Services e podem ser implantados usando MDSModelDeploy.exe.|[Implantando exemplos de MDS no SQL Server](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)|
  
 Caso você tenha problemas durante o processo de instalação ou na configuração inicial, veja [Solucionando problemas de instalação e configuração](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) no Wiki do TechNet.  
  
 Se não precisar mais do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador, você pode desinstalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e determinar se deverão ser removidos os itens que não são afetados pelo processo de desinstalação. Para obter mais informações, veja [Desinstalar e remover o Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
