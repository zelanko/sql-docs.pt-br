---
title: Propriedades MSReportServer_ConfigurationSetting | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Properties
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c38f439e53f3efd60b60ae026f485b61ecb9ee0c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277418"
---
# <a name="msreportserverconfigurationsetting-properties"></a>Propriedades MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting representa os parâmetros de instalação e de tempo de execução de uma instância do servidor de relatório. Essas configurações são armazenadas no arquivo de configuração RSReportServer.config.  
  
## <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|Retorna o tamanho de pool de conexão usado pelo servidor de relatório para se comunicar com a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|Especifica a conta de logon usada pelo servidor de relatório para se conectar à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|Especifica o número de segundos de espera antes de uma tentativa de logon no banco de dados do servidor de relatório falhar. Somente leitura.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|Especifica se o servidor de relatório usa uma conta de serviço do Windows, uma conta de usuário do Windows ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|Especifica o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|Especifica o número de segundos que devem decorrer antes de o comando falhar ou expirar. O servidor de relatório está cronometrando o processo no catálogo do SQL Server, não uma fonte de dados para o relatório.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|Especifica o nome do servidor em que o banco de dados do servidor de relatório está instalado.|  
|[Propriedade InstallationID](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|Retorna um identificador exclusivo para uma instância de servidor de relatório específica.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|Especifica o nome de uma instância do servidor de relatório em um computador específico.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|Indica se a instância do servidor de relatório foi inicializada.  Somente leitura.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|Indica se o servidor de relatório está configurado para o modo integrado do SharePoint.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|Indica se o serviço Web Servidor de Relatórios está habilitado. Somente leitura.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|Indica se o serviço do Windows do servidor de relatório está habilitado. Somente leitura.|  
|[Propriedade MachineAccountIdentity &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|Obtém a identidade da conta da máquina do computador em que o servidor de relatório está instalado.|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|Especifica o caminho de instalação para uma instância do servidor de relatório.|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|Retorna o nível de conexão segura especificado no arquivo RSReportServer.config.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|Obtém o endereço usado para enviar e-mail do servidor de relatório. Somente leitura.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|Especifica se a propriedade SendUsing na configuração de e-mail está definida como TRUE.|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|Obtém a propriedade do servidor SMTP do arquivo RSReportServer.config. Somente leitura.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|Especifica a conta do usuário de logon que o servidor de relatório representa durante a execução de relatórios autônomos. Somente leitura.|  
|[Versão](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|Retorna a versão do servidor de relatório.|  
|[Propriedade VirtualDirectoryReportManager &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|Retorna o diretório virtual para o aplicativo do gerenciador de relatórios.|  
|[Propriedade VirtualDirectoryReportServer &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|Retorna o diretório virtual para o aplicativo do serviço Web Servidor de Relatórios.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório está sendo executado efetivamente. Somente leitura.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório foi configurada por último para executar. Somente leitura.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  
