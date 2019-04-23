---
title: Métodos MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Methods
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2e9abd4e72182bb649eb608a2f7a7e2bef7044f9
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59936933"
---
# <a name="msreportserverconfigurationsetting-methods"></a>Métodos MSReportServer_ConfigurationSetting
  A classe MSReportServer_ConfigurationSetting do Provedor WMI do servidor de relatório fornece os métodos públicos a seguir.  
  
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
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|Retorna um conjunto de tokens que representam as versões do Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.|  
|[Método ListIPAddresses &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|Lista endereços IP para o computador.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|Retorna uma lista de instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de essas instalações terem acesso a informações seguras.|  
|[Método ListReservedURLs &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|Lista as URLs reservadas para todos os aplicativos no servidor de relatório.|  
|[Método ListSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|Lista as associações de certificado SSL que existem no HTTP.SYS e as que são esperadas do RSReportServer.config.|  
|[Método ListSSLCertificates &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|Lista certificados SSL instalados no computador.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no banco de dados do servidor de relatório que usa essa nova chave.|  
|[Método RemoveSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|Remove uma associação do Certificado SSL.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|Exclui a entrada da conta da execução autônoma da configuração do servidor de relatório.|  
|[Método RemoveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|Remove uma URL reservada para o servidor de relatório.|  
|[Método ReserveURL &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|Adiciona uma reserva de URL para um determinado aplicativo.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|Reaplica a chave de criptografia especificada para o banco de dados do servidor de relatório.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|Especifica o valor de tempo limite padrão para as tentativas de logon do banco de dados do servidor de relatório.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|Especifica o valor de tempo limite padrão para consultas no banco de dados do servidor de relatório.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|Configura a extensão de entrega de email usada pelo servidor de relatório para enviar email.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|Define o nível de conexão segura do servidor de relatório.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|Ativa e desativa o serviço do servidor de relatório.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|Especifica a conta usada para executar relatórios autônomos.|  
|[Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|Define o diretório virtual para um aplicativo.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|Faz com que o serviço do Servidor de Relatório seja executado como o usuário especificado do Windows e concede a esta conta permissões no sistema de arquivos suficientes para o funcionamento do servidor de relatório.|  
  
## <a name="see-also"></a>Consulte também  
 [MSReportServer_ConfigurationSetting Class](msreportserver-configurationsetting-class.md)  
  
  
