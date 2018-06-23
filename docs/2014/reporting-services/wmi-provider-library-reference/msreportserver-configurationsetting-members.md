---
title: Membros MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
caps.latest.revision: 46
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 32a253a22466d154c5e7e0fc3bb355c20c0f0847
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008837"
---
# <a name="msreportserverconfigurationsetting-members"></a>Membros MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting contém as seguintes propriedades e métodos.  
  
## <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|Retorna o tamanho de pool de conexão usado pelo servidor de relatório para se comunicar com a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|Especifica a conta de logon usada pelo servidor de relatório para se conectar à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|Especifica o número de segundos de espera antes de uma tentativa de logon no banco de dados do servidor de relatório falhar. Somente leitura.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|Especifica se o servidor de relatório usa uma conta de serviço do Windows, uma conta de usuário do Windows ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseName](configurationsetting-property-databasename.md)|Especifica o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|Especifica o número de segundos que devem decorrer antes de o comando falhar ou expirar. O servidor de relatório está cronometrando o processo no banco de dados do servidor de relatório, não uma fonte de dados para o relatório.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|Especifica o nome do servidor em que o banco de dados do servidor de relatório está instalado.|  
|[Propriedade InstallationID](configurationsetting-property-installationid.md)|Retorna um identificador exclusivo para uma instância de servidor de relatório específica.|  
|[InstanceName](configurationsetting-property-instancename.md)|Especifica o nome de uma instância do servidor de relatório em um computador específico.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|Indica se a instância do servidor de relatório foi inicializada. Somente leitura.|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|Indica se o servidor de relatório está configurado para o modo integrado do SharePoint.|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|Indica se o serviço Web Servidor de Relatórios está habilitado. Somente leitura.|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|Indica se o serviço do Windows do servidor de relatório está habilitado. Somente leitura.|  
|[Propriedade MachineAccountIdentity &#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|Obtém a identidade da conta da máquina do computador em que o servidor de relatório está instalado.|  
|[PathName](configurationsetting-property-pathname.md)|Especifica o caminho de instalação para uma instância do servidor de relatório.|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|Retorna o nível de conexão segura especificado no arquivo RSReportServer.config.|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|Obtém o endereço usado para enviar e-mail do servidor de relatório. Somente leitura.|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|Especifica se a propriedade SendUsing na configuração de e-mail está definida como TRUE.|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|Obtém a propriedade do servidor SMTP do arquivo RSReportServer.config. Somente leitura.|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|Especifica a conta do usuário de logon que o servidor de relatório representa durante a execução de relatórios autônomos. Somente leitura.|  
|[Versão](configurationsetting-property-version.md)|Retorna a versão do servidor de relatório.|  
|[Propriedade VirtualDirectoryReportManager &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|Retorna o diretório virtual para o aplicativo do gerenciador de relatórios.|  
|[Propriedade VirtualDirectoryReportServer &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|Retorna o diretório virtual para o aplicativo do serviço Web Servidor de Relatórios.|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório está sendo executado efetivamente. Somente leitura.|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório foi configurada por último para executar. Somente leitura.|  
  
## <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|Efetua backup da chave de criptografia para a instância. A chave de criptografia é armazenada criptografada com uma senha.|  
|[Método CreateSSLCertificateBinding &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-createsslcertificatebinding.md)|Cria uma associação de Certificado SSL.|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|Exclui as informações criptografadas do banco de dados do servidor de relatório.|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|Exclui as chaves de criptografia do banco de dados do servidor de relatório.|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|Gera um Script SQL que pode ser usado para criar o banco de dados do servidor de relatório.|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|Gera um script SQL que pode ser usado para conceder permissões de usuário ao banco de dados do servidor de relatório.|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|Gera um Script SQL que pode ser usado para atualizar um banco de dados do servidor de relatório.|  
|[Método GetAdminSiteUrl &#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|Obtém a URL absoluta para o site da Web da Administração Central.|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|Obtém o nome para exibição para uma determinada cadeia de caracteres da versão do banco de dados do servidor de relatório.|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|Inicializa a instância do servidor de relatório especificado.|  
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|Retorna um conjunto de tokens que representam as versões do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.|  
|[Método ListIPAddresses &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|Lista endereços IP para o computador.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|Retorna uma lista de instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de essas instalações terem acesso a informações seguras.|  
|[Método ListReservedURLs &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|Lista as URLs reservadas para todos os aplicativos no servidor de relatório.|  
|[Método ListSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|Lista as associações de certificado SSL que existem no HTTP.SYS e as que são esperadas do rsreportserver.config.|  
|[Método ListSSLCertificates &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|Lista certificados SSL instalados no computador.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no banco de dados do servidor de relatório que usa essa nova chave.|  
|[Método RemoveSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|Remove uma associação do Certificado SSL.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|Exclui a entrada da conta da execução autônoma da configuração do servidor de relatório.|  
|[Método RemoveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|Remove uma URL reservada para o servidor de relatório.|  
|[Método ReserveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|Adiciona uma reserva de URL para um determinado aplicativo.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|Reaplica a chave de criptografia especificada para o banco de dados do servidor de relatório.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|Especifica o valor de tempo limite padrão para as tentativas de logon do banco de dados do servidor de relatório.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|Especifica o valor de tempo limite padrão para as conexões do banco de dados do servidor de relatório.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|Configura a extensão de entrega de email usada pelo servidor de relatório para enviar email.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|Define o nível de conexão segura do servidor de relatório.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|Ativa e desativa o Servidor de Relatório do Windows e os serviços Web.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|Especifica a conta usada para executar relatórios autônomos.|  
|[Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|Define o diretório virtual para um aplicativo.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|Faz com que o serviço Servidor de Relatório do Windows seja executado como o usuário do Windows especificado e concede a esta conta permissões no sistema de arquivos suficientes para o funcionamento do servidor de relatório.|  
  
## <a name="see-also"></a>Consulte também  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
  