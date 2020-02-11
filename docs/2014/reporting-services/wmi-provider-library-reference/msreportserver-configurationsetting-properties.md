---
title: Propriedades MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c3937d888089f06435fece25e791b10ebbab785
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097325"
---
# <a name="msreportserver_configurationsetting-properties"></a>Propriedades MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting representa os parâmetros de instalação e de runtime de uma instância do servidor de relatório. Essas configurações são armazenadas no arquivo de configuração RSReportServer.config.  
  
## <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|Retorna o tamanho do pool de conexões usado pelo servidor de relatório para se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] comunicar com a instância que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|Especifica a conta de logon usada pelo servidor de relatório para se conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] à instância do que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|Especifica o número de segundos de espera antes de uma tentativa de logon no banco de dados do servidor de relatório falhar. Somente leitura.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|Especifica se o servidor de relatório usa uma conta de serviço do Windows, uma conta de usuário do Windows ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseName](configurationsetting-property-databasename.md)|Especifica o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|Especifica o número de segundos que devem decorrer antes que o comando falhe ou expire. O servidor de relatório está cronometrando o processo no catálogo de SQL Server, não uma fonte de dados para o relatório.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|Especifica o nome do servidor em que o banco de dados do servidor de relatório está instalado.|  
|[Propriedade InstallationID](configurationsetting-property-installationid.md)|Retorna um identificador exclusivo para uma instância de servidor de relatório específica.|  
|[InstanceName](configurationsetting-property-instancename.md)|Especifica o nome de uma instância do servidor de relatório em um computador específico.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|Indica se a instância do servidor de relatório foi inicializada.  Somente leitura.|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|Indica se o servidor de relatório está configurado para o modo integrado do SharePoint.|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|Indica se o serviço Web Servidor de Relatórios está habilitado. Somente leitura.|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|Indica se o serviço do Windows do servidor de relatório está habilitado. Somente leitura.|  
|[Propriedade MachineAccountIdentity &#40;&#41;WMI](configurationsetting-property-machineaccountidentity.md)|Obtém a identidade da conta da máquina do computador em que o servidor de relatório está instalado.|  
|[PathName](configurationsetting-property-pathname.md)|Especifica o caminho de instalação para uma instância do servidor de relatório.|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|Retorna o nível de conexão segura especificado no arquivo RSReportServer.config.|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|Obtém o endereço usado para enviar e-mail do servidor de relatório. Somente leitura.|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|Especifica se a propriedade SendUsing na configuração de e-mail está definida como TRUE.|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|Obtém a propriedade do servidor SMTP do arquivo RSReportServer.config. Somente leitura.|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|Especifica a conta do usuário de logon que o servidor de relatório representa durante a execução de relatórios autônomos. Somente leitura.|  
|[Versão](configurationsetting-property-version.md)|Retorna a versão do servidor de relatório.|  
|[Propriedade VirtualDirectoryReportManager &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|Retorna o diretório virtual para o aplicativo do gerenciador de relatórios.|  
|[Propriedade VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|Retorna o diretório virtual para o aplicativo do serviço Web Servidor de Relatórios.|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório está sendo executado efetivamente. Somente leitura.|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório foi configurada por último para executar. Somente leitura.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
