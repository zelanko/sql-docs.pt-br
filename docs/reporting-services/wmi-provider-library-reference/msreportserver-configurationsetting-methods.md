---
title: "M&#233;todos MSReportServer_ConfigurationSetting | Microsoft Docs"
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
  - "MSReportServer_ConfigurationSetting Methods"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Provedor WMI [Reporting Services], classe MSReportServer_ConfigurationSetting"
  - "Classe MSReportServer_ConfigurationSetting"
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# M&#233;todos MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting do Provedor WMI do servidor de relatório fornece os métodos públicos a seguir.  
  
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
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/listinstalledsharepointversions-method-wmi.md)|Retorna um conjunto de tokens que representam as versões do Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.|  
|[Método ListIPAddresses &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listipaddresses-method-wmi-msreportserver-configurationsetting.md)|Lista endereços IP para o computador.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/listreportserversindatabase-method-wmi-msreportserver-configurationsetting.md)|Retorna uma lista de instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de essas instalações terem acesso a informações seguras.|  
|[Método ListReservedURLs &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listreservedurls-method-wmi-msreportserver-configurationsetting.md)|Lista as URLs reservadas para todos os aplicativos no servidor de relatório.|  
|[Método ListSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Lista as associações de certificado SSL que existem no HTTP.SYS e as que são esperadas do RSReportServer.config.|  
|[Método ListSSLCertificates &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificates-method-wmi-msreportserver-configurationsetting.md)|Lista certificados SSL instalados no computador.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/reencryptsecureinformation-method-wmi-msreportserver-configurationsetting.md)|Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no banco de dados do servidor de relatório que usa essa nova chave.|  
|[Método RemoveSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removesslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Remove uma associação do Certificado SSL.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/removeunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Exclui a entrada da conta da execução autônoma da configuração do servidor de relatório.|  
|[Método RemoveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removeurl-method-wmi-msreportserver-configurationsetting.md)|Remove uma URL reservada para o servidor de relatório.|  
|[Método ReserveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md)|Adiciona uma reserva de URL para um determinado aplicativo.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/restoreencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Reaplica a chave de criptografia especificada para o banco de dados do servidor de relatório.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/setdatabaseconnection-method-wmi-msreportserver-configurationsetting.md)|Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/setdatabaselogontimeout-method-wmi-msreportserver-configurationsetting.md)|Especifica o valor de tempo limite padrão para as tentativas de logon do banco de dados do servidor de relatório.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/setdatabasequerytimeout-method-wmi-msreportserver-configurationsetting.md)|Especifica o valor de tempo limite padrão para consultas no banco de dados do servidor de relatório.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/setemailconfiguration-method-wmi-msreportserver-configurationsetting.md)|Configura a extensão de entrega de email usada pelo servidor de relatório para enviar email.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/setsecureconnectionlevel-method-wmi-msreportserver-configurationsetting.md)|Define o nível de conexão segura do servidor de relatório.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/setservicestate-method-wmi-msreportserver-configurationsetting.md)|Ativa e desativa o serviço do servidor de relatório.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/setunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Especifica a conta usada para executar relatórios autônomos.|  
|[Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md)|Define o diretório virtual para um aplicativo.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/setwindowsserviceidentity-method-wmi-msreportserver-configurationsetting.md)|Faz com que o serviço do Servidor de Relatório seja executado como o usuário especificado do Windows e concede a esta conta permissões no sistema de arquivos suficientes para o funcionamento do servidor de relatório.|  
  
## Consulte também  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  