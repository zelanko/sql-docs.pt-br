---
title: "Atualizar um banco de dados do servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 89bb5de5f669d033dd18bc63e11ef5bd29644542
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---

# <a name="upgrade-a-report-server-database"></a>Atualizar um banco de dados do servidor de relatório

O banco de dados do servidor de relatório fornece armazenamento para uma ou mais instâncias do servidor de relatório. Como o esquema do banco de dados do servidor de relatório pode ser alterado a cada versão nova do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é necessário que a versão do banco de dados corresponda à versão da instância do servidor de relatório que você está usando. Na maioria dos casos, um banco de dados do servidor de relatório pode ser atualizado automaticamente sem ação específica de sua parte.  
  
 **Modo nativo:** no modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o banco de dados do servidor de relatório é realmente composto de dois bancos de dados que têm os nomes padrão de “ReportServer e ReportServerTempDB.”  
  
 **Modo do SharePoint:** no modo do SharePoint do SQL Server 2016 Reporting Services do report Server banco de dados é na verdade uma coleção de bancos de dados é criada para cada instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço.  

## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>Maneiras de atualizar um banco de dados do servidor de relatório de modo nativo

 A seguinte lista identifica as condições nas quais um banco de dados do servidor de relatório é atualizado:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualiza uma única instância de um servidor de relatório. O esquema de banco de dados do servidor de relatório é atualizado automaticamente após a inicialização do serviço, e o servidor de relatório determina que a versão do esquema de banco de dados não corresponde à do servidor.  
  
     Durante a inicialização do serviço, o servidor de relatório verifica se a versão do esquema de banco de dados corresponde à versão do servidor. Se a versão do esquema de banco de dados for mais antiga, ela será atualizada automaticamente para a versão de esquema exigida pelo servidor de relatório. A atualização automática é especialmente útil se você restaurou ou anexou um banco de dados de servidor de relatório mais antigo. Uma mensagem é inserida no arquivo de log de rastreamento do servidor de relatório, indicando que a versão do esquema de banco de dados foi atualizada.  
  
-   O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] atualiza um banco de dados do servidor de relatório local ou remoto quando você seleciona uma versão mais antiga a ser usada com uma instância mais recente do servidor de relatório. Nesse caso, você deve confirmar a ação de atualização antes que ela aconteça.  
  
     O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece mais um botão Atualizar separado ou um script de atualização. Esses recursos ficaram obsoletos a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] devido ao recurso de atualização automática do serviço Servidor de Relatório.  
  
 Depois que o esquema for atualizado, você não poderá reverter a atualização para uma versão anterior. Sempre faça backup do banco de dados do servidor de relatório, caso precise recriar uma instalação anterior.  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>Como o esquema, os metadados e o conteúdo do servidor de relatório são atualizados  
 O banco de dados do servidor de relatório é atualizado em três estágios:  
  
1.  O esquema é atualizado automaticamente após a instalação e a inicialização do serviço ou quando você seleciona um banco de dados do servidor de relatório do modo nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é uma versão antiga. Além disso, o serviço do Servidor de Relatório verifica a versão do banco de dados durante a inicialização. Se o servidor de relatório estiver conectado a um banco de dados que seja de uma versão anterior, o servidor de relatório atualizará o banco de dados durante a inicialização.  
  
2.  Os descritores de segurança são atualizados durante o primeiro uso do banco de dados do servidor de relatório após a atualização do esquema.  
  
3.  Os relatórios publicados e os instantâneos de relatório compilados são atualizados durante o primeiro uso. Para obter mais informações, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
 Além do banco de dados do servidor de relatório, um servidor de relatório também usa um banco de dados temporário. O banco de dados temporário é atualizado automaticamente quando você atualiza o banco de dados do servidor de relatório.  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>Permissões necessárias para atualizar um banco de dados do Servidor de Relatório  
 Se você estiver atualizando uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contenha um banco de dados do servidor de relatório, poderá ver uma mensagem de erro se a atualização de banco de dados for executada com permissões insuficientes. Por padrão, a Instalação usa o token de segurança do usuário que está executando o programa Instalação para se conectar à instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e atualizar o esquema. Se você tiver permissões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** no servidor de banco de dados que hospeda os bancos de dados do servidor de relatório, a atualização do banco de dados será bem-sucedida. Da mesma maneira, se você executar a Instalação no prompt de comando e especificar os argumentos RSUPGRADEDATABASEACCOUNT e RSUPGRADEPASSWORD para uma conta que tem a permissão de **sysadmin** para modificar o esquema no computador remoto, a atualização do banco de dados será bem-sucedida.  
  
 Todavia, se você não tiver permissão de **sysadmin** no banco de dados do computador remoto, a conexão será recusada com o seguinte erro:  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 Nesse ponto, os arquivos de programas do servidor de relatório serão atualizados, mas o banco de dados do servidor de relatório estará no formato da versão anterior. O servidor de relatório ficará indisponível até que você conclua o processo de atualização por meio da atualização manual do banco de dados.  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>Para atualizar um banco de dados de modo nativo com scripts  
 Você pode usar scripts do WMI para atualizar um banco de dados do servidor de relatórios. Para obter mais informações, consulte [Método GenerateDatabaseUpgradeScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)  
  
## <a name="next-steps"></a>Próximas etapas

[Gerenciador de configuração do Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[Criar um banco de dados do servidor de relatório](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
[Assistente de banco de dados de alteração](http://msdn.microsoft.com/library/1a2e8d18-5997-482f-a9c1-87d99f7407b8)   
[Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Migrar uma instalação do Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
