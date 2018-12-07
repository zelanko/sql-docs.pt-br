---
title: Instalar o Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 486e4216-a946-4c6e-828c-61bc905f7ec1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 273d0e9df4a5cd5a2649fcd8ada4fe9891393dcd
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617936"
---
# <a name="install-data-quality-services"></a>Instalar o Data Quality Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversionLong](../../includes/ssdqsnoversionlong-md.md)] (DQS) contém os dois componentes a seguir: **[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]** e **[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]**.  
  
|Componente DQS|Descrição|  
|-------------------|-----------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] é instalado sobre o Mecanismo de Banco de Dados do [!INCLUDE[ssNoversion](../../includes/ssNoVersion-md.md)] e inclui três bancos de dados: DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA. O DQS_MAIN contém procedimentos armazenados do DQS, o mecanismo DQS e bases de dados de conhecimento publicadas. O DQS_PROJECTS contém as informações sobre o projeto de qualidade de dados. DQS_STAGING_DATA é a área de preparo onde você pode copiar seus dados de origem para executar operações de DQS e, depois, exportar os dados processados.|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] é um aplicativo autônomo que o habilita a se conectar ao [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. Ele fornece uma interface gráfica do usuário altamente intuitiva para executar operações de qualidade de dados e outras tarefas administrativas relacionadas ao DQS.|  
  
> [!IMPORTANT]  
>  Além dos dois componentes DQS anteriores, você também pode:  
>   
>  Usar a Transformação de Limpeza DQS no Integration Services que executa a limpeza de dados no processo de empacotamento do Integration Services e é instalado automaticamente quando você instala o Integration Services. Para obter informações sobre a instalação do Integration Services, consulte [Instalar o Integration Services](../../integration-services/install-windows/install-integration-services.md).  
>   
>  Habilitar a integração de DQS no Master Data Services para usar a funcionalidade de correspondência do DQS no Suplemento Master Data Services para Excel. Para obter mais informações, consulte [Habilitar a integração do Data Quality Services com Master Data Services](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 A instalação do DQS é um processo de três partes:  
  
-   [Tarefas pré-instalação](#PreInstallationTasks): verificar os requisitos do sistema antes da instalação do DQS.  
  
-   [Tarefas de instalação do Data Quality Services](#DQSInstallation): instale o DQS na Instalação do SQL Server.  
  
-   [Tarefas de pós-instalação](#PostInstallationTasks): execute essas tarefas depois de concluir a Instalação do SQL Server para concluir a instalação do DQS.  
  
> [!NOTE]  
>  Este tópico não inclui instruções para a execução da Instalação pela linha de comando. Para obter informações sobre opções de linha de comando para instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] e o cliente, consulte [Parâmetros de recursos](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Feature) em [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
##  <a name="PreInstallationTasks"></a> Tarefas pré-instalação  
 Antes de instalar o DQS, verifique se o computador atende aos requisitos mínimos do sistema. A tabela a seguir especifica informações sobre os requisitos mínimos do sistema para os componentes DQS:  
  
|Componente DQS|Requisitos mínimos do sistema|  
|-------------------|---------------------------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|Memória (RAM): mínima: 2 GB/recomendada: 4 GB ou mais<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] . Para obter mais informações, consulte [Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md).|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|.NET Framework 4.0 (instalado durante a instalação do [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] , se ainda não estiver instalado)<br /><br /> Internet Explorer 6.0 SP1 ou posterior|  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] e [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] podem ser instalados no mesmo computador ou em computadores diferentes. Os dois componentes podem ser instalados de forma independente um do outro e em qualquer sequência. Entretanto, para usar o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], será necessário um [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] instalado ao qual se conectar.  
>   
>  Você pode se conectar à versão do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando a versão atual ou anterior do [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] e a Transformação de Limpeza DQS. Para obter informações sobre como atualizar sua versão existente do DQS para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], consulte [Atualizar o Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
>   
>  Embora a Microsoft Excel não seja um pré-requisito para instalar o Cliente Data Quality, o Microsoft Excel 2003 ou posterior deve ser instalado no computador do Cliente Data Quality para executar várias operações no aplicativo cliente como importar valores de domínio de um arquivo do Excel ou mapear para os dados de origem em um arquivo do Excel para descoberta de conhecimento, limpeza ou atividades de correspondência.  
  
 Para obter informações detalhadas sobre os requisitos mínimos do sistema para a instalação do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], confira [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
##  <a name="DQSInstallation"></a> Tarefas de instalação do Data Quality Services  
 Você deve usar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] para instalar componentes do DQS. Quando você executar a Instalação do SQL Server, deverá passar por uma série de páginas do assistente de instalação para selecionar opções apropriadas com base nos requisitos. A tabela a seguir lista somente as páginas do assistente de instalação em que as opções selecionadas afetarão a instalação do DQS:  
  
|Página|Ação|  
|----------|------------|  
|Seleção de recursos|Selecione:<br /><br /> **Data Quality Services** em **Serviços de Mecanismo de Banco de Dados** para instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. <br />Se você marcar a caixa de seleção **Data Quality Services** , a Instalação do SQL Server copiará um arquivo do instalador, o DQSInstaller.exe, no diretório da instância do SQL Server no computador. Execute esse arquivo depois de concluir a Instalação do SQL Server para *concluir* a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Será necessário também executar algumas etapas adicionais para configurar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] antes de poder usá-lo. Para obter mais informações, consulte [Tarefas pós-instalação](#PostInstallationTasks).<br /><br /> **Cliente Data Quality** para instalar o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].<br /><br /> (Recomendado) **Ferramentas de Gerenciamento – Completas** em **Ferramentas de Gerenciamento – Básicas** para instalar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Fornecem uma interface do usuário gráfica para gerenciar a instância do SQL Server e ajudam a executar tarefas adicionais pós-instalação, como listado na próxima seção.|  
|Configuração do Mecanismo de Banco de Dados|Clique em **Adicionar Usuário Atual** para adicionar sua conta de usuário do Windows à função de servidor fixa sysadmin. Isso é necessário para você poder executar o arquivo DQSInstaller.exe posteriormente para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .|  
  
##  <a name="PostInstallationTasks"></a> Tarefas de pós-instalação  
 Depois de concluir o assistente de instalação do SQL Server, execute as etapas adicionais mencionadas nesta seção para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , configurá-lo e usá-lo.  
  
1.  Para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , execute o arquivo DQSInstaller.exe. Ao executar o arquivo DQSInstaller.exe:  
  
    -   Os bancos de dados DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA são criados.  
  
    -   Os logons ##MS_dqs_db_owner_login## e ##MS_dqs_service_login## são criados.  
  
    -   As funções dqs_administrator, dqs_kb_editor e dqs_kb_operator são criadas no banco de dados DQS_MAIN.  
  
    -   O procedimento armazenado DQInitDQS_MAIN é criado no banco de dados mestre.  
  
    -   O arquivo DQS_install.log é geralmente criado na pasta C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.*<instance_name>* \MSSQL\Log. O arquivo contém informações sobre as ações necessárias para executar o arquivo DQSInstaller.exe.  
  
    -   Se um banco de dados do Master Data Services estiver presente na mesma instância do SQL Server que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], um usuário mapeado para o logon de Master Data Services será criado e receberá a função dqs_administrator no banco de dados DQS_MAIN.  
  
     Isso conclui a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
     Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
2.  Conceder funções DQS a usuários:  
  
     Para fazer logon no [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], um usuário deve ter quaisquer das três funções a seguir no banco de dados DQS_MAIN:  
  
    -   **dqs_administrator**  
  
    -   **dqs_kb_editor**  
  
    -   **dqs_kb_operator**  
  
     Por padrão, se sua conta de usuário for um membro da função de servidor fixa sysadmin, você poderá fazer logon no [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] mesmo que nenhuma das funções de DQS seja concedida à sua conta de usuário. Para obter mais informações sobre as três funções DQS, consulte [DQS Security](../../data-quality-services/dqs-security.md).  
  
     Para obter mais informações, consulte [Grant DQS Roles to Users](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md).  
  
    > [!NOTE]  
    >  As três funções DQS não estão disponíveis para os bancos de dados DQS_PROJECTS e DQS_STAGING_DATA.  
  
3.  Disponibilize seus dados para operações do DQS. Verifique se você pode acessar seus dados de origem para as operações do DQS e se pode exportar os dados processados para uma tabela em um banco de dados.  
  
     Para obter mais informações, consulte  
                    [Acessar dados para as operações do DQS](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Vídeo: Instalar e configurar o DQS](https://go.microsoft.com/fwlink/?LinkId=238241)   
 [Atualizar assemblies SQLCLR após atualizar o .NET Framework](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [Exportar e importar bases de dados de conhecimento DQS usando o DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)   
 [Atualizar o Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)   
 [Remover objetos do Data Quality Server](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Instalar os recursos do business intelligence do SQL Server](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
 [Desinstalar o SQL Server](../../sql-server/install/uninstall-sql-server.md)   
 [Data Quality Services](../../data-quality-services/data-quality-services.md)   
 [Solução de problemas de instalação e de configuração no DQS](https://social.technet.microsoft.com/wiki/contents/articles/3776.aspx)  
  
  
