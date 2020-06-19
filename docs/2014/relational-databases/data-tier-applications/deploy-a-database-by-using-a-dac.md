---
title: Implantar um banco de dados usando um DAC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbdeployment.settings.f1
- sql12.swb.dbdeployment.progress.f1
- sql12.swb.dbdeployment.summary.f1
- sql12.swb.dbdeployment.results.f1
- sql12.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
author: stevestein
ms.author: sstein
ms.openlocfilehash: c0da23febcc1f2e97b1dfaff29a5df5ced16c7e4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970266"
---
# <a name="deploy-a-database-by-using-a-dac"></a>Implantar um banco de dados usando um DAC
  Use o Assistente **Implantar Banco de Dados no SQL Azure** para implantar um banco de dados entre uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e um servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ou entre dois servidores [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeBegin"></a> Antes de começar  
 O assistente usa um arquivo morto BACPAC DAC (aplicativo da camada de dados) para implantar os dados e as definições dos objetos de banco de dados. Ele executa uma operação de exportação de DAC do banco de dados de origem, e uma importação de DAC para o destino.  
  
###  <a name="database-options-and-settings"></a><a name="DBOptSettings"></a> Opções e configurações de banco de dados  
 Por padrão, o banco de dados criado durante a implantação terá todas as configurações padrão da instrução CREATE DATABASE. A exceção é que a ordenação e o nível de compatibilidade do banco de dados estão definidos como valores do banco de dados de origem.  
  
 As opções de banco de dados, como TRUSTWORTHY, DB_CHAINING e HONOR_BROKER_PRIORITY, não podem ser ajustadas como parte do processo de implantação. Propriedades físicas, como o número de grupos de arquivos ou os números e os tamanhos de arquivos, não podem ser alteradas como parte do processo de implantação. Após a conclusão da implantação, você pode usar a instrução ALTER DATABASE, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar o banco de dados.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 O assistente para **Implantar Banco de Dados** oferece suporte à implantação de um banco de dados:  
  
-   De uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
-   Do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] para uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Entre dois servidores [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .  
  
 O assistente não oferece suporte à implantação de bancos de dados entre duas instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve estar executando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior para funcionar com o assistente. Se um banco de dados em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiver objetos sem suporte no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você não poderá usar o assistente para implantar o banco de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Se um banco de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] contiver objetos sem suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você não poderá usar o assistente para implantar o banco de dados nas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para melhorar a segurança, os logons de Autenticação do SQL Server são armazenados em um arquivo BACPAC DAC sem senha. Quando o arquivo BACPAC é importado, o logon é criado como um logon desabilitado com uma senha gerada. Para habilitar os logons, faça logon usando um logon que tenha a permissão de ALTER ANY LOGIN e use ALTER LOGIN para habilitar o logon e atribuir uma nova senha que possa ser comunicada ao usuário. Isso não é necessário para logons de Autenticação do Windows porque suas senhas não são gerenciadas pelo SQL Server.  
  
#### <a name="permissions"></a>Permissões  
 O assistente requer permissões de exportação de DAC no banco de dados de origem. O logon exige pelo menos as permissões ALTER ANY LOGIN e VIEW DEFINITION no escopo do banco de dados, bem como as permissões SELECT em **sys.sql_expression_dependencies**. A exportação de um DAC pode ser feita por membros da função de servidor fixa securityadmin que também são membros da função de banco de dados fixa database_owner no banco de dados do qual o DAC é exportado. Membros da função de servidor fixa sysadmin ou da conta interna do administrador do sistema do SQL Server denominada **sa** também podem exportar um DAC.  
  
 O assistente requer permissões de importação de DAC no servidor ou na instância de destino. O logon deve ser um membro das funções de servidor fixas **sysadmin** ou **serveradmin** , ou da função de servidor fixa **dbcreator** e ter as permissões ALTER ANY LOGIN. A conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada **sa** também pode importar um DAC. A importação de um DAC com logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige associação nas funções loginmanager ou serveradmin. A importação de um DAC sem logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige a associação nas funções dbmanager ou serveradmin.  
  
##  <a name="using-the-deploy-database-wizard"></a><a name="UsingDeployDACWizard"></a> Usando o Assistente para Implantar Banco de Dados  
 **Para migrar um banco de dados usando o Assistente para Implantar Banco de dados**  
  
1.  Conecte-se ao local do banco de dados que você deseja implantar. Você pode especificar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou um servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .  
  
2.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o banco de dados.  
  
3.  Expanda o nó **Bancos de Dados** .  
  
4.  Clique com o botão direito do mouse no banco de dados que deseja implantar, selecione **Tarefas**e selecione **Implantar Banco de Dados no SQL Azure...**  
  
5.  Conclua as etapas das caixas de diálogo do assistente:  
  
    -   [Página de Introdução](#Introduction)  
  
    -   [Configurações de Implantação](#Deployment_settings)  
  
    -   [Página de Resumo](#Summary)  
  
    -   [Resultados](#Results)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas do Assistente para **Implantar Banco de Dados** .  
  
 **Opções**  
  
-   **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página de Introdução no futuro.  
  
-   **Avançar** - Continua na página **Configurações de Implantação** .  
  
-   **Cancelar** – cancela a operação e fecha o assistente.  
  
##  <a name="deployment-settings-page"></a><a name="Deployment_settings"></a>Página Configurações de implantação  
 Use esta página para especificar o servidor de destino e fornecer detalhes sobre seu novo banco de dados.  
  
 **Host local:**  
  
-   **Conexão do servidor** – especifique os detalhes de conexão do servidor e clique em **conectar** para verificar a conexão.  
  
-   **Nome do novo banco de dados** – especifique um nome para o novo banco de dados.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]configurações do banco de dados:**  
  
-   ** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] edição** – selecione a edição do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no menu suspenso.  
  
-   **Tamanho máximo do banco de dados** – selecione o tamanho máximo do banco de dados no menu suspenso.  
  
 **Outras configurações:**  
  
-   Especifique um diretório local para o arquivo temporário, que é o arquivo morto BACPAC. Observe que o arquivo será criado no local especificado e permanecerá lá depois que a operação for concluída.  
  
##  <a name="summary-page"></a><a name="Summary"></a> Página de Resumo  
 Use esta página para analisar a origem especificada e as configurações de destino para a operação. Para concluir a operação de implantação usando as configurações especificadas, clique em **Concluir**. Para cancelar a operação de implantação e sair do Assistente, clique em **Cancelar**.  
  
##  <a name="progress-page"></a><a name="Progress"></a> Página Progresso  
 Esta página exibe a barra de progresso que indica o status da operação. Para exibir o status detalhado, clique na opção **Exibir detalhes** .  
  
##  <a name="results-page"></a><a name="Results"></a>Página de resultados  
 Esta página reporta o êxito ou falha da operação de implantação, mostrando os resultados de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Clique no link para exibir um relatório do erro para essa ação.  
  
 Clique em **concluir** para fechar o assistente.  
  
## <a name="using-a-net-framework-application"></a>Usando um aplicativo .NET Framework  
 **Para implantar um banco de dados usando os métodos DacStoreExport() e Import() em um aplicativo .Net Framework.**  
  
 Para exibir um exemplo de código, baixe o aplicativo de exemplo do DAC em [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575)  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância ou o servidor que contém o banco de dados a ser implantado.  
  
2.  Abra um objeto `ServerConnection` e conecte-se à mesma instância.  
  
3.  Use o método `Export` do tipo `Microsoft.SqlServer.Management.Dac.DacStore` para exportar o banco de dados para um arquivo BACPAC. Especifique o nome do banco de dados a ser exportado e o caminho para a pasta onde o arquivo BACPAC será colocado.  
  
4.  Crie um objeto de servidor SMO e defina-o como a instância ou o servidor de destino.  
  
5.  Abra um objeto `ServerConnection` e conecte-se à mesma instância.  
  
6.  Use o método `Import` do tipo `Microsoft.SqlServer.Management.Dac.DacStore` para importar o BACPAC. Especifique o arquivo BACPAC criado pela exportação.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da camada de dados](data-tier-applications.md)   
 [Exportar um aplicativo da camada de dados](export-a-data-tier-application.md)   
 [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
