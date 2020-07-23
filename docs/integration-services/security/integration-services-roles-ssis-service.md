---
title: Funções do Integration Services (Serviço SSIS) | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86ebb4c5420b1fa7abcbae00a190f11023b73b0b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922067"
---
# <a name="integration-services-roles-ssis-service"></a>Funções do Integration Services (Serviço do SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece certas funções fixas no nível de banco de dados para ajudar a proteger o acesso a pacotes que estão armazenados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As funções disponíveis são diferentes dependendo se você estiver salvando pacotes no SSISDB (banco de dados de Catálogo do SSIS) ou no banco de dados msdb.  
  
## <a name="roles-in-the-ssis-catalog-database-ssisdb"></a>Funções do SSISDB (banco de dados de Catálogo do SSIS)  
 O SSISDB (banco de dados de Catálogo do SSIS) fornece as funções fixas de nível de banco de dados a seguir para ajudar a proteger o acesso a pacotes e informações sobre pacotes.  
  
-   **ssis_admin**. Essa função fornece acesso administrativo completo ao banco de dados de Catálogo do SSIS.  
  
-   **ssis_logreader** Essa função fornece permissões para acessar todos os modos de exibição relacionados a logs operacionais do SSISDB.  
  
     A lista de modos de exibição inclui: [catalog].[projects], [catalog].[packages], [catalog].[operations], [catalog].[extended_operation_info], [catalog].[operation_messages], [catalog].[event_messages], [catalog].[execution_data_statistics], [catalog].[execution_component_phases], [catalog].[execution_data_taps], [catalog].[event_message_context], [catalog].[executions], [catalog].[executables], [catalog].[executable_statistics], [catalog].[validations], [catalog].[execution_parameter_values] e [catalog].[execution_property_override_values].  
  
## <a name="roles-in-the-msdb-database"></a>Funções do banco de dados msdb  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui as três funções fixas no nível de banco de dados, **db_ssisadmin**, **db_ssisltduser** e **db_ssisoperator**, para controlar o acesso a pacotes que são salvos no banco de dados **msdb**. Você atribui funções a um pacote por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As tarefas das funções são salvas no banco de dados **msdb** .  
  
### <a name="read-and-write-actions"></a>Ações de leitura e gravação  
 A tabela a seguir descreve as ações de leitura e gravação do Windows e as funções fixas no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Função|Ação de leitura|Ação de gravação|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> ou<br /><br /> **sysadmin**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar os próprios pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Excluir todos os pacotes.<br /><br /> Mudar as funções dos próprio pacotes.<br /><br /> Alterar as funções de todos os pacotes.<br /><br /> <br /><br /> **\*\* Aviso \*\*** Os membros das funções db_ssisadmin e dc_admin podem estar aptos a elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.|  
|**db_ssisltduser**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Exportar os próprios pacotes.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Mudar as funções dos próprio pacotes.|  
|**db_ssisoperator**|Enumerar todos os pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Nenhum|  
|**Administradores do Windows**|Exibir os detalhes de execução de todos os pacotes em execução.|Parar todos os pacotes em execução.|  
  
### <a name="sysssispackages-table"></a>Tabela Sysssispackages  
 A tabela **sysssispackages** no **msdb** contém os pacotes que foram salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md).  
  
 A tabela **sysssispackages** inclui colunas que contêm informações sobre as funções atribuídas aos pacotes.  
  
-   A coluna **readerrole** especifica a função que tem acesso de leitura ao pacote.  
  
-   A coluna **writerrole** especifica a função que tem acesso de gravação ao pacote.  
  
-   A coluna **ownersid** contém o identificador de segurança exclusivo do usuário que criou o pacote. Essa coluna define o proprietário do pacote.  
  
### <a name="permissions"></a>Permissões  
 Por padrão, as permissões do **db_ssisadmin** , as funções fixas no nível de banco de dados do **db_ssisoperator** e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de leitura dos pacotes, e as permissões da função **db_ssisadmin** e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de gravação. Um usuário deve ser um membro da função **db_ssisadmin**, **db_ssisltduser**ou **db_ssisoperator** para ter acesso de leitura ao pacote. Um usuário deve ser membro da função **db_ssisadmin** para ter acesso de gravação.  
  
### <a name="access-to-packages"></a>Acesso a pacotes  
 As funções fixas no nível de banco de dados trabalham em conjunto com as funções definidas pelo usuário. As funções definidas pelo usuário são as funções criadas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e então usadas para atribuir permissões aos pacotes. Para acessar um pacote, um usuário deve ser membro da função definida pelo usuário e da função fixa no nível de banco de dados pertinente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por exemplo, se os usuários forem membros da função definida pelo usuário **AuditUsers** atribuída a um pacote, eles também deverão ser membros da função **db_ssisadmin**, **db_ssisltduser**ou **db_ssisoperator** para terem acesso de leitura ao pacote.  
  
 Se você não atribuir funções definidas pelo usuário aos pacotes, o acesso aos pacotes será determinado pelas funções fixas no nível do banco de dados.  
  
 Se você quiser usar funções definidas pelo usuário, precisará adicioná-las ao banco de dados **msdb** antes de atribuí-las aos pacotes. Você pode criar funções de banco de dados novas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 As funções em nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] concedem direitos nas tabelas do sistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o serviço do MSSQLSERVER) deve ser iniciado antes de você se conectar ao Mecanismo de Banco de Dados e acessar o banco de dados **msdb** .  
  
 Para atribuir funções a pacotes, você precisa concluir as seguintes tarefas.  
  
-   **Abrir o Pesquisador de Objetos e conectar-se ao Integration Services**  
  
     Para poder atribuir funções aos pacotes por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve abrir o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve ser iniciado antes de você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Atribuir funções de leitor e de gravador aos pacotes**  
  
     Você pode atribuir uma função de leitor e de gravador a cada pacote.  

## <a name="assign-a-reader-and-writer-role-to-a-package"></a><a name="assign"></a> Atribuir uma função de leitor e de gravador a um pacote
  Você pode atribuir uma função de leitor e de gravador a cada pacote.  
  
### <a name="assign-a-reader-and-writer-role-to-a-package"></a>Atribuir uma função de leitor e de gravador a um pacote  
  
1.  No Pesquisador de Objetos, localize a conexão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Expanda a pasta Pacotes Armazenados e, depois, expanda a subpasta que contém o pacote ao qual você deseja atribuir funções.  
  
3.  Clique com o botão direito do mouse no pacote ao qual você deseja atribuir funções.  
  
4.  Na caixa de diálogo **Funções do Pacote** , selecione uma função de leitor na lista **Função de Leitor** e uma função de gravador na lista **Função de Gravador** .  
  
5.  Clique em **OK**.

## <a name="create-a-user-defined-role"></a><a name="create"></a> Criar uma função definida pelo usuário
    
### <a name="to-create-a-user-defined-role"></a>Para criar uma função definida pelo usuário  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Clique em **Pesquisador de Objetos** no menu **Exibir** .  
  
3.  Na barra de ferramentas do Pesquisador de Objetos, clique em **Conectar**e clique em **Mecanismo de Banco de Dados**.  
  
4.  Na caixa de diálogo **Conectar ao Servidor** , forneça um nome de um servidor e selecione um modo de autenticação. Você pode usar um ponto (.), (local) ou **localhost** para indicar o servidor local.  
  
5.  Clique em **Conectar**.  
  
6.  Expanda Bancos de Dados, Bancos de Dados do Sistema, msdb, Segurança e Funções.  
  
7.  No nó Funções, clique com o botão direito do mouse em Funções de Banco de Dados e clique em **Nova Função de Banco de Dados**.  
  
8.  Na página Geral, forneça um nome e, opcionalmente, especifique um proprietário e esquemas proprietários e adicione membros da função.  
  
9. Opcionalmente, clique em **Permissões** e configure as permissões de objeto.  
  
10. Opcionalmente, clique em **Propriedades Estendidas** e configure qualquer propriedade estendida.  
  
11. Clique em **OK**.

## <a name="package-roles-dialog-box-ui-reference"></a><a name="roles_dialog"></a> Referência da interface do usuário da caixa de diálogo Funções do Pacote
  Use a caixa de diálogo **Funções do Pacote** , disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para especificar as funções de nível de banco de dados que têm acesso de leitura e as que têm acesso de gravação ao pacote. As funções de nível de banco de dados se aplicam apenas a pacotes armazenados no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**msdb**.  
  
 As funções listadas na caixa de diálogo são as funções de banco de dados atuais do banco de dados de sistema **msdb** . Se nenhuma função for selecionada, serão aplicadas as funções do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por padrão, a função de leitor inclui **db_ssisadmin**, **db_ssisoperator**e o usuário que criou o pacote. Um usuário membro de uma dessas funções ou criador dos pacotes pode enumerar, exibir, exportar e executar pacotes. Por padrão, a função de gravador inclui **db_ssisadmin** e o usuário que criou o pacote. Um usuário membro dessa função e o criador dos pacotes podem importar, excluir e alterar pacotes.  
  
 A coluna **ownersid** da tabela **sysssispackages** lista o identificador de segurança exclusivo do usuário que criou o pacote.  
  
### <a name="options"></a>Opções  
 **Nome do Pacote**  
 Especifique o nome do pacote.  
  
 **Função de Leitor**  
 Selecione uma função na lista.  
  
 **Função de Gravador**  
 Selecione uma função na lista  
