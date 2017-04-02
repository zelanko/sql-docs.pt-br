---
title: "Fun&#231;&#245;es do Integration Services (Servi&#231;o do SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "segurança [Integration Services], funções"
  - "função db_ssisoperator"
  - "função db_ssisadmin"
  - "funções fixas de banco de dados [Integration Services]"
  - "pacotes [Integration Services], segurança"
  - "funções [Integration Services]"
  - "função db_ssisltduser"
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Fun&#231;&#245;es do Integration Services (Servi&#231;o do SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece certas funções fixas no nível de banco de dados para ajudar a proteger o acesso a pacotes armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As funções disponíveis são diferentes dependendo se você estiver salvando pacotes no SSISDB (banco de dados de Catálogo do SSIS) ou no banco de dados msdb.  
  
## Funções do SSISDB (banco de dados de Catálogo do SSIS)  
 O SSISDB (banco de dados de Catálogo do SSIS) fornece as funções fixas de nível de banco de dados a seguir para ajudar a proteger o acesso a pacotes e informações sobre pacotes.  
  
-   **ssis_admin**. Essa função fornece acesso administrativo completo ao banco de dados de Catálogo do SSIS.  
  
-   **ssis_logreader** Essa função fornece permissões para acessar todos os modos de exibição relacionados a logs operacionais do SSISDB.  
  
     A lista de modos de exibição inclui: [catalog].[projects], [catalog].[packages], [catalog].[operations], [catalog].[extended_operation_info], [catalog].[operation_messages], [catalog].[event_messages], [catalog].[execution_data_statistics], [catalog].[execution_component_phases], [catalog].[execution_data_taps], [catalog].[event_message_context], [catalog].[executions], [catalog].[executables], [catalog].[executable_statistics], [catalog].[validations], [catalog].[execution_parameter_values] e [catalog].[execution_property_override_values].  
  
## Funções do banco de dados msdb  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui as três funções fixas de nível de banco de dados, **db_ssisadmin**, **db_ssisltduser** e **db_ssisoperator**, para controlar o acesso a pacotes que são salvos no banco de dados **msdb**. Você atribui funções a um pacote por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As tarefas das funções são salvas no banco de dados **msdb** .  
  
### Ações de leitura e gravação  
 A tabela a seguir descreve as ações de leitura e gravação do Windows e as funções fixas no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Função|Ação de leitura|Ação de gravação|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> ou<br /><br /> **sysadmin**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar os próprios pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Excluir todos os pacotes.<br /><br /> Mudar as funções dos próprio pacotes.<br /><br /> Alterar as funções de todos os pacotes.<br /><br /> <br /><br /> **\*\* Aviso \*\***Os membros das funções db_ssisadmin e dc_admin podem estar aptos a elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.|  
|**db_ssisltduser**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Exportar os próprios pacotes.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Mudar as funções dos próprio pacotes.|  
|**db_ssisoperator**|Enumerar todos os pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Nenhum.|  
|**Administradores do Windows**|Exibir os detalhes de execução de todos os pacotes em execução.|Parar todos os pacotes em execução.|  
  
### Tabela Sysssispackages  
 A tabela **sysssispackages** no **msdb** contém os pacotes que foram salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md).  
  
 A tabela **sysssispackages** inclui colunas que contêm informações sobre as funções atribuídas aos pacotes.  
  
-   A coluna **readerrole** especifica a função que tem acesso de leitura ao pacote.  
  
-   A coluna **writerrole** especifica a função que tem acesso de gravação ao pacote.  
  
-   A coluna **ownersid** contém o identificador de segurança exclusivo do usuário que criou o pacote. Essa coluna define o proprietário do pacote.  
  
### Permissões  
 Por padrão, as permissões do **db_ssisadmin**, as funções fixas no nível de banco de dados do **db_ssisoperator** e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de leitura dos pacotes, e as permissões da função **db_ssisadmin** e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de gravação. Um usuário deve ser um membro da função **db_ssisadmin**, **db_ssisltduser** ou **db_ssisoperator** para ter acesso de leitura ao pacote. Um usuário deve ser membro da função **db_ssisadmin** para ter acesso de gravação.  
  
### Acesso a pacotes  
 As funções fixas no nível de banco de dados trabalham em conjunto com as funções definidas pelo usuário. As funções definidas pelo usuário são as funções criadas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e então usadas para atribuir permissões aos pacotes. Para acessar um pacote, um usuário deve ser membro da função definida pelo usuário e da função fixa no nível de banco de dados pertinente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Por exemplo, se os usuários forem membros da função definida pelo usuário **AuditUsers** atribuída a um pacote, eles também deverão ser membros da função **db_ssisadmin**, **db_ssisltduser** ou **db_ssisoperator** para terem acesso de leitura ao pacote.  
  
 Se você não atribuir funções definidas pelo usuário aos pacotes, o acesso aos pacotes será determinado pelas funções fixas no nível do banco de dados.  
  
 Se você quiser usar funções definidas pelo usuário, precisará adicioná-las ao banco de dados **msdb** antes de atribuí-las aos pacotes. Você pode criar funções de banco de dados novas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 As funções em nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] concedem direitos nas tabelas do sistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o serviço do MSSQLSERVER) deve ser iniciado antes de você se conectar ao Mecanismo de Banco de Dados e acessar o banco de dados **msdb**.  
  
 Para atribuir funções a pacotes, você precisa concluir as seguintes tarefas.  
  
-   **Abrir o Pesquisador de Objetos e conectar-se ao Integration Services**  
  
     Para poder atribuir funções aos pacotes por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve abrir o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve ser iniciado antes de você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Atribuir funções de leitor e de gravador aos pacotes**  
  
     Você pode atribuir uma função de leitor e de gravador a cada pacote.  
  
## Tarefas relacionadas  
  
-   [Atribuir uma função de leitor e de gravador a um pacote](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Criar uma função definida pelo usuário](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Conectar-se ao Integration Services](../../integration-services/service/connect-to-integration-services.md)  
  
  