---
title: "Membros MSReportServer_ConfigurationSetting | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "MSReportServer_ConfigurationSetting Members"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Provedor WMI [Reporting Services], classe MSReportServer_ConfigurationSetting"
  - "Classe MSReportServer_ConfigurationSetting"
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
caps.latest.revision: 46
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 46
---
# Membros MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting contém as seguintes propriedades e métodos.  
  
## Propriedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/connectionpoolsize-property-wmi-msreportserver-configurationsetting.md)|Retorna o tamanho de pool de conexão usado pelo servidor de relatório para se comunicar com a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md)|Especifica a conta de logon usada pelo servidor de relatório para se conectar à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/databaselogontimeout-property-wmi-msreportserver-configurationsetting.md)|Especifica o número de segundos de espera antes de uma tentativa de logon no banco de dados do servidor de relatório falhar. Somente leitura.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md)|Especifica se o servidor de relatório usa uma conta de serviço do Windows, uma conta de usuário do Windows ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/databasename-property-wmi-msreportserver-configurationsetting.md)|Especifica o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/databasequerytimeout-property-wmi-msreportserver-configurationsetting.md)|Especifica o número de segundos que devem decorrer antes de o comando falhar ou expirar. O servidor de relatório está cronometrando o processo no banco de dados do servidor de relatório, não uma fonte de dados para o relatório.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/databaseservername-property-wmi-msreportserver-configurationsetting.md)|Especifica o nome do servidor em que o banco de dados do servidor de relatório está instalado.|  
|[Propriedade InstallationID](../../reporting-services/wmi-provider-library-reference/installationid-property-wmi-msreportserver-configurationsetting.md)|Retorna um identificador exclusivo para uma instância de servidor de relatório específica.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/instancename-property-wmi-msreportserver-configurationsetting.md)|Especifica o nome de uma instância do servidor de relatório em um computador específico.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/isinitialized-property-wmi-msreportserver-configurationsetting.md)|Indica se a instância do servidor de relatório foi inicializada. Somente leitura.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/issharepointintegrated-property-wmi.md)|Indica se o servidor de relatório está configurado para o modo integrado do SharePoint.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/iswebserviceenabled-property-wmi-msreportserver-configurationsetting.md)|Indica se o serviço Web Servidor de Relatórios está habilitado. Somente leitura.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/iswindowsserviceenabled-property-wmi-msreportserver-configurationsetting.md)|Indica se o serviço do Windows do servidor de relatório está habilitado. Somente leitura.|  
|[Propriedade MachineAccountIdentity &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/machineaccountidentity-property-wmi.md)|Obtém a identidade da conta da máquina do computador em que o servidor de relatório está instalado.|  
|[PathName](../../reporting-services/wmi-provider-library-reference/pathname-property-wmi-msreportserver-configurationsetting.md)|Especifica o caminho de instalação para uma instância do servidor de relatório.|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/secureconnectionlevel-property-wmi-msreportserver-configurationsetting.md)|Retorna o nível de conexão segura especificado no arquivo RSReportServer.config.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/senderemailaddress-property-wmi-msreportserver-configurationsetting.md)|Obtém o endereço usado para enviar e-mail do servidor de relatório. Somente leitura.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/sendusingsmtpserver-property-wmi-msreportserver-configurationsetting.md)|Especifica se a propriedade SendUsing na configuração de e-mail está definida como TRUE.|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/smtpserver-property-wmi-msreportserver-configurationsetting.md)|Obtém a propriedade do servidor SMTP do arquivo RSReportServer.config. Somente leitura.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/unattendedexecutionaccount-property-wmi-msreportserver-configurationsetting.md)|Especifica a conta do usuário de logon que o servidor de relatório representa durante a execução de relatórios autônomos. Somente leitura.|  
|[Versão](../../reporting-services/wmi-provider-library-reference/version-property-wmi-msreportserver-configurationsetting.md)|Retorna a versão do servidor de relatório.|  
|[Propriedade VirtualDirectoryReportManager &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportmanager-property-wmi-msreportserver-configurationsetting.md)|Retorna o diretório virtual para o aplicativo do gerenciador de relatórios.|  
|[Propriedade VirtualDirectoryReportServer &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportserver-property-wmi-msreportserver-configurationsetting.md)|Retorna o diretório virtual para o aplicativo do serviço Web Servidor de Relatórios.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityactual-property-wmi-msreportserver-configurationsetting.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório está sendo executado efetivamente. Somente leitura.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Retorna a identidade sob a qual o serviço do Windows do servidor de relatório foi configurada por último para executar. Somente leitura.|  
  
## Métodos públicos  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/backupencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Efetua backup da chave de criptografia para a instância. A chave de criptografia é armazenada criptografada com uma senha.|  
|[Método CreateSSLCertificateBinding &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/createsslcertificatebinding-method-wmi-msreportserver-configurationsetting.md)|Cria uma associação de Certificado SSL.|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/deleteencryptedinformation-method-wmi-msreportserver-configurationsetting.md)|Exclui as informações criptografadas do banco de dados do servidor de relatório.|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/deleteencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Exclui as chaves de criptografia do banco de dados do servidor de relatório.|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/generatedatabasecreationscript-method-wmi-msreportserver-configurationsetting.md)|Gera um Script SQL que pode ser usado para criar o banco de dados do servidor de relatório.|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/generatedatabaserightsscript-method-wmi-msreportserver-configurationsetting.md)|Gera um script SQL que pode ser usado para conceder permissões de usuário ao banco de dados do servidor de relatório.|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/generatedatabaseupgradescript-method-wmi-msreportserver-configurationsetting.md)|Gera um Script SQL que pode ser usado para atualizar um banco de dados do servidor de relatório.|  
|[Método GetAdminSiteUrl &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/getadminsiteurl-method-wmi.md)|Obtém a URL absoluta para o site da Web da Administração Central.|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/getdatabaseversiondisplayname-method-wmi.md)|Obtém o nome para exibição para uma determinada cadeia de caracteres da versão do banco de dados do servidor de relatório.|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/initializereportserver-method-wmi-msreportserver-configurationsetting.md)|Inicializa a instância do servidor de relatório especificado.|  
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/listinstalledsharepointversions-method-wmi.md)|Retorna um conjunto de tokens que representam as versões do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.|  
|[Método ListIPAddresses &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listipaddresses-method-wmi-msreportserver-configurationsetting.md)|Lista endereços IP para o computador.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/listreportserversindatabase-method-wmi-msreportserver-configurationsetting.md)|Retorna uma lista de instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de essas instalações terem acesso a informações seguras.|  
|[Método ListReservedURLs &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listreservedurls-method-wmi-msreportserver-configurationsetting.md)|Lista as URLs reservadas para todos os aplicativos no servidor de relatório.|  
|[Método ListSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Lista as associações de certificado SSL que existem no HTTP.SYS e as que são esperadas do rsreportserver.config.|  
|[Método ListSSLCertificates &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificates-method-wmi-msreportserver-configurationsetting.md)|Lista certificados SSL instalados no computador.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/reencryptsecureinformation-method-wmi-msreportserver-configurationsetting.md)|Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no banco de dados do servidor de relatório que usa essa nova chave.|  
|[Método RemoveSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removesslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Remove uma associação do Certificado SSL.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/removeunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Exclui a entrada da conta da execução autônoma da configuração do servidor de relatório.|  
|[Método RemoveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removeurl-method-wmi-msreportserver-configurationsetting.md)|Remove uma URL reservada para o servidor de relatório.|  
|[Método ReserveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md)|Adiciona uma reserva de URL para um determinado aplicativo.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/restoreencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Reaplica a chave de criptografia especificada para o banco de dados do servidor de relatório.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/setdatabaseconnection-method-wmi-msreportserver-configurationsetting.md)|Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/setdatabaselogontimeout-method-wmi-msreportserver-configurationsetting.md)|Especifica o valor de tempo limite padrão para as tentativas de logon do banco de dados do servidor de relatório.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/setdatabasequerytimeout-method-wmi-msreportserver-configurationsetting.md)|Especifica o valor de tempo limite padrão para as conexões do banco de dados do servidor de relatório.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/setemailconfiguration-method-wmi-msreportserver-configurationsetting.md)|Configura a extensão de entrega de email usada pelo servidor de relatório para enviar email.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/setsecureconnectionlevel-method-wmi-msreportserver-configurationsetting.md)|Define o nível de conexão segura do servidor de relatório.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/setservicestate-method-wmi-msreportserver-configurationsetting.md)|Ativa e desativa o Servidor de Relatório do Windows e os serviços Web.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/setunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Especifica a conta usada para executar relatórios autônomos.|  
|[Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md)|Define o diretório virtual para um aplicativo.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/setwindowsserviceidentity-method-wmi-msreportserver-configurationsetting.md)|Faz com que o serviço Servidor de Relatório do Windows seja executado como o usuário do Windows especificado e concede a esta conta permissões no sistema de arquivos suficientes para o funcionamento do servidor de relatório.|  
  
## Consulte também  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  