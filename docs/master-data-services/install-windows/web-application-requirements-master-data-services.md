---
title: Requisitos do aplicativo Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- master data services
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
caps.latest.revision: 40
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2f2c480d3d600e409557d82d55ead7febfc82c1
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="web-application-requirements-master-data-services"></a>Requisitos do aplicativo Web (Master Data Service)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] é um aplicativo Web hospedado pelo IIS (Serviços de Informações da Internet). [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] funciona apenas no Internet Explorer (IE) 9 ou posterior. Não há suporte para o IE 8 e versões anteriores, para o Microsoft Edge e o Chrome.  

**Para obter instruções sobre como instalar e configurar o IIS**, consulte [Instalando e configurando o IIS](../../master-data-services/master-data-services-installation-and-configuration.md#InstallIIS).
  
 Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar e configurar o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] configura o IIS no computador local; portanto, ele é ideal para tarefas de configuração inicial da Web. Por exemplo, configure um ambiente do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] com um único aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ou configure o primeiro aplicativo Web em uma implantação em expansão do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Use ferramentas do IIS para executar tarefas mais complexas, como, por exemplo, configurar vários servidores Web em uma implantação em expansão.  
  
> [!NOTE]  
>  Qualquer computador em que os componentes do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] deve ser licenciado. Para obter mais informações, consulte o Contrato de Licença de Usuário Final (EULA).  
  
## <a name="requirements"></a>Requisitos  
  
### <a name="operating-system"></a>Sistema operacional  
 Antes de instalar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], examine os seguintes requisitos:    
    
-   [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 Para trabalhar no aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , o Silverlight 5 deve estar instalado no computador cliente. Se você não tiver a versão exigida do Silverlight, será solicitado a instalá-la quando navegar até uma área do aplicativo Web que a exige. Você pode instalar o Silverlight 5 por [aqui](http://go.microsoft.com/fwlink/?LinkId=243096).  
  
### <a name="role-and-role-services"></a>Função e serviços de função  
 No Windows Server 2012 ou no Windows Server 2012 R2, você pode usar o **Gerenciador do Servidor**, que está disponível no MMC (Console de Gerenciamento Microsoft), para instalar a função **Servidor Web (IIS)** e os serviços de função necessários.  
 
 
> [!IMPORTANT]  
>A**Compactação de Conteúdo Dinâmico** é habilitada por padrão. Isso reduz consideravelmente o tamanho da resposta xml e salva a E/S de rede, embora o uso da CPU aumente.  Para obter mais informações, veja **Melhoria do desempenho do [CTP] 2.0** em [Novidades no MDS &#40;Master Data Services&#41;](../../master-data-services/what-s-new-in-master-data-services-mds.md).  
  
||  
|-|  
|Serviços de Informações da Internet<br /><br /> Ferramentas de gerenciamento da Web<br /><br /> Console de Gerenciamento IIS<br /><br /> Serviços da World Wide Web<br /><br /> Desenvolvimento de aplicativo<br /><br /> .NET Extensibility 3.5<br /><br /> Extensibilidade do .NET 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> Extensões ISAPI<br /><br /> Filtros ISAPI<br /><br /> Recursos comuns de HTTP<br /><br /> Documento padrão<br /><br /> Navegação de diretório<br /><br /> Erros de HTTP<br /><br /> Conteúdo estático<br /><br /> [Observação: não instale a Publicação WebDAV]<br /><br /> Integridade e diagnóstico<br /><br /> Log de HTTP<br /><br /> Monitor de solicitação<br /><br /> Desempenho<br /><br /> Compactação de conteúdo estático<br /><br /> Segurança<br /><br /> Filtragem de solicitação<br /><br /> Autenticação do Windows|  
  
### <a name="features"></a>Recursos 
 No Windows Server 2012 ou no Windows Server 2012 R2, você pode usar o **Gerenciador do Servidor** para instalar os recursos necessários a seguir.  
  
||  
|-|  
|.NET Framework 3.5 (inclui o .NET 2.0 e 3.0)<br /><br /> Serviços avançados do .NET Framework 4.5<br /><br /> ASP.NET 4.5<br /><br /> Serviços WCF<br /><br /> Ativação de HTTP [Observação: isso é necessário.]<br /><br /> Compartilhamento de porta TCP<br /><br /> Serviço de Ativação de Processos do Windows<br /><br /> Modelo de processo<br /><br /> Ambiente .NET<br /><br /> APIs de configuração<br/><br/>Compactação de Conteúdo Dinâmico|  
  
 Veja a seguir um exemplo de script do PowerShell para adicionar os recursos e funções do servidor de pré-requisito. Os recursos e as funções de servidor de pré-requisito variam conforme o ambiente.  
  
```powershell  
Install-WindowsFeature Web-Mgmt-Console, AS-NET-Framework, Web-Asp-Net, Web-Asp-Net45, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Http-Logging, Web-Request-Monitor, Web-Stat-Compression, Web-Filtering, Web-Windows-Auth, NET-Framework-Core, WAS-Process-Model, WAS-NET-Environment, WAS-Config-APIs  
  
Install-WindowsFeature Web-App-Dev, NET-Framework-45-Features -IncludeAllSubFeature –Restart  
```  
  
 Para obter mais informações sobre o comando do PowerShell, confira [Install-WindowsFeature](https://technet.microsoft.com/library/jj205467).  
  
### <a name="accounts-and-permissions"></a>Contas e permissões  
  
|Tipo|Description|  
|----------|-----------------|  
|Conta do Windows|Você deve fazer logon no computador do servidor Web com uma conta do Windows que tenha permissão para configurar funções, serviços de função e recursos do Windows e para criar e gerenciar pools de aplicativos, sites e aplicativos Web no IIS no computador local.|  
|Conta de serviço|Quando você criar o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], especifique uma identidade para o pool de aplicativos em que o aplicativo é executado. Esta conta pode ser diferente da conta de serviço especificada quando o banco de dados [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] foi criado.<br /><br /> Essa identidade deve ser uma conta de usuário de domínio e é acrescentada à função de banco de dados mds_exec no banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para acesso ao banco de dados. Para obter mais informações, veja [Logons, usuários e funções de banco de dados](../../master-data-services/database-logins-users-and-roles-master-data-services.md). Essa conta também é adicionada a um grupo do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no Windows, **MDS_ServiceAccounts**, que recebe permissão para o diretório temporário de compilação, **MDSTempDir**, no sistema de arquivos. Para obter mais informações, veja [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
      
 [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [Página Configuração da Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
