---
title: Instalar o Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7eb8d46339849b0f4c6baeca7d1b78e0ef29ab47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020955"
---
# <a name="install-master-data-services"></a>Instalar o Master Data Services
  O fluxo de trabalho a seguir fornece uma visão geral de como instalar e configurar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a instalação é um processo de três partes:  
  
-   [Tarefas pré-instalação](#preinstall): verificar os requisitos do sistema antes da instalação do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
-   [Operações de Instalação](#install): instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o prompt de comando.  
  
-   [Tarefas pós-instalação](#postinstall): abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para concluir operações pós-instalação. Criar e configurar o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web, e implantar um modelo de exemplo.  
  
##  <a name="preinstall"></a> Tarefas pré-instalação  
  
|Ação|Detalhes|Tópicos relacionados|  
|------------|-------------|--------------------|  
|Verificar os requisitos de instalação|O computador onde a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada deve atender aos requisitos mínimos de:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalação.<br /><br /> O Aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web.<br /><br /> O banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , se for hospedado no mesmo computador do aplicativo Web.<br /><br /> Observe que você pode separar o computador do servidor web e o computador do servidor de banco de dados executando a instalação somente o computador do servidor web e criando o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] banco de dados em um computador remoto que executa uma versão com suporte e a edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)<br /><br /> [Requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Requisitos do aplicativo de Web &#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)<br /><br /> [Requisitos de banco de dados &#40;Master Data Services&#41;](database-requirements-master-data-services.md)|  
|Configurar as funções, serviços de função e recursos necessários|Antes de executar a Instalação, configure o computador com as funções, serviços de função e recursos necessários do Windows.<br /><br /> Observação: embora esta etapa possa ser executada posteriormente no fluxo de trabalho, é útil configurar isso antes de executar a Instalação para que você possa executar as tarefas de configuração da Web imediatamente após a instalação.|[Requisitos do aplicativo de Web &#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)|  
|Revisar as considerações de suporte a idioma|Determine o idioma em que deseja instalar e executar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Implantações multilíngues e globais &#40;Master Data Services&#41;](multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> Operações de Instalação  
  
|Ação|Detalhes|Tópicos relacionados|  
|------------|-------------|--------------------|  
|Execute a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|No computador que hospedará o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e os serviços Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , use a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um prompt de comando para instalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Ao usar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponível na página **Seleção de Recursos** , em **Recursos Compartilhados**. Ao usar um prompt de comando, o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponível como um parâmetro de recurso. Observe que o processo de instalação de linha de comando instala o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], mas não o configura. Você deve configurá-lo usando o Gerenciador de Configurações do Master Data Services. O processo de instalação:<br /><br /> Instala as pastas e arquivos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no local especificado para recursos compartilhados e atribui permissões a esses objetos.<br /><br /> Registra os assemblies do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no GAC (Cache de Assembly Global).<br /><br /> Instala o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].|[Instalar o SQL Server 2014 do Assistente de instalação &#40;instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> Tarefas pós-instalação  
  
|Ação|Detalhes|Tópicos relacionados|  
|------------|-------------|--------------------|  
|Abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para concluir operações pós-instalação.|Após a conclusão da instalação, abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] executa as seguintes operações de pós-instalação no computador local:<br /><br /> Cria um grupo do Windows, **MDS_ServiceAccounts**, para conter contas de serviço do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para pools de aplicativos.<br /><br /> No caminho de instalação do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , cria a pasta MDSTempDir e atribui permissões para **MDS_ServiceAccounts**. É nessa pasta que são compilados arquivos de compilação temporários para o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] configura o arquivo Web. config, o `tempDirectory` atributo o  **\<compilação >** elemento com o caminho para a pasta MDSTempDir.<br /><br /> <br /><br /> Se você gerar script do processo de instalação, poderá abrir o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para registrar o snap-in do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], mas terá que executar as outras etapas manualmente para concluir a configuração. O [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] fornece um processo de configuração dirigido por assistente. Não há nenhum processo de linha de comando para configurar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|[Permissões de pasta e arquivo &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)<br /><br /> [Referência de configuração Web &#40;Master Data Services&#41;](../web-configuration-reference-master-data-services.md)|  
|Criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para seus dados mestres.|[Criar um banco de dados do Master Data Services](create-a-master-data-services-database.md)|  
|Criar um aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar e configurar um aplicativo Web que hospedará o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|[Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)|  
|Associar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a um aplicativo Web|Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para associar o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ao banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Associar um banco de dados do Master Data Services a um aplicativo Web](associate-a-master-data-services-database-and-web-application.md)|  
|Configurar a segurança aprimorada do Internet Explorer|Quando você instala o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador Windows Server 2008 ou Windows Server 2008 R2, talvez você precise configurar o Internet Explorer Enhanced Security para permitir script para o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] site de aplicativo. Caso contrário, haverá falha ao navegar até o site de aplicativo do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] no computador de servidor.|[Internet Explorer: configuração de segurança aprimorada](http://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|Instalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|Os usuários que trabalharão com dados mestre podem instalar o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)].|[http://go.microsoft.com/fwlink/?LinkId=219530](http://go.microsoft.com/fwlink/?LinkId=219530)|  
|Habilitar a integração do DQS (Data Quality Services)|Para usuários do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], habilite a integração com o recurso DQS que pode ser usado para fazer a correspondência de dados semelhantes.|[Habilitar a integração do Data Quality Services com Master Data Services](enable-data-quality-services-integration-with-master-data-services.md)|  
|Implantar um modelo de exemplo|Pacotes de modelo de exemplo são instalados com o Master Data Services e podem ser implantados usando MDSModelDeploy.exe.|[Implantando exemplos de MDS no SQL Server](http://go.microsoft.com/fwlink/?LinkId=251486&clcid=0x409)|  
  
 Caso você tenha problemas durante o processo de instalação ou na configuração inicial, veja [Solucionando problemas de instalação e configuração](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) no Wiki do TechNet.  
  
 Se não precisar mais do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador, você pode desinstalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e determinar se deverão ser removidos os itens que não são afetados pelo processo de desinstalação. Para obter mais informações, veja [Desinstalar e remover o Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  