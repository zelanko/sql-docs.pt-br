---
title: "Catálogo do SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.iscreatecatalog.f1
- sql13.ssis.ssms.iscatalogprop.general.f1
- sql13.ssis.dbupgradewizard.f1
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 3e2139cf2c56b1f716aac32aa6b3f71cb49a2d61
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---

# <a name="ssis-catalog"></a>Catálogo do SSIS
  O catálogo do **SSISDB** é o ponto central para trabalhar com projetos do [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] (SSIS) que você implantou no servidor [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]. Por exemplo, você define parâmetros de projeto e pacote, configura ambientes para especificar valores de tempo de execução para pacotes, executa e soluciona problemas de pacotes, e gerencia as operações de servidor do [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] .  
  
 Os objetos armazenados no catálogo **SSISDB** incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 Você inspeciona objetos, configurações e dados operacionais que são armazenados no catálogo do **SSISDB** , consultando as exibições no banco de dados **SSISDB** . Você gerencia os objetos chamando procedimentos armazenados no banco de dados **SSISDB** ou usando a interface de usuário do catálogo **SSISDB** . Em muitos casos, a mesma tarefa pode ser executada na interface de usuário ou chamando um procedimento armazenado.  
  
 Para manter o banco de dados **SSISDB** , é recomendado que você aplique políticas empresariais padrão para gerenciar os bancos de dados de usuários. Para obter informações sobre como criar planos de manutenção, consulte [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md).  
  
 O catálogo **SSISDB** e o banco de dados **SSISDB** dão suporte ao Windows PowerShell. Para obter mais informações sobre como usar o SQL Server com Windows PowerShell, consulte [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md). Para obter exemplos de como usar o Windows PowerShell para concluir tarefas como implantar um projeto, consultar a entrada de blog, [SSIS e PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539)em blogs.msdn.com.  
  
 Para obter mais informações sobre como exibir dados de operações, consulte [Monitorar pacote em execução e outras operações](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
 Você acessa o catálogo **SSISDB** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conectando-se ao Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e expandindo o nó **Catálogos do Integration Services** no Pesquisador de Objetos. Você acessa o banco de dados **SSISDB** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] expandindo o nó Bancos de Dados no Pesquisador de Objetos.  
  
> [!NOTE]
> Não é possível renomear o banco de dados **SSISDB** .  
  
> [!NOTE]
> Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual o banco de dados **SSISDB** está anexado para ou não responde, o processo ISServerExec.exe termina. Uma mensagem é gravada em um log de Eventos do Windows.  
>   
>  Se os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizarem failover como parte de um failover de cluster, os pacotes de execução não serão reiniciados. Você pode usar pontos de verificação para reiniciar pacotes. Para saber mais, confira [Reiniciar pacotes por meio de pontos de verificação](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="features-and-capabilities"></a>Recursos e funcionalidades  
  
-   [Identificadores de objetos do catálogo](../../integration-services/service/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [Configuração do catálogo](../../integration-services/service/ssis-catalog.md#Configuration)  
  
-   [Permissões](../../integration-services/service/ssis-catalog.md#Permissions)  
  
-   [Pastas](../../integration-services/service/ssis-catalog.md#Folders)  
  
-   [Projetos e pacotes](../../integration-services/service/ssis-catalog.md#ProjectsAndPackages)  
  
-   [Parâmetros](../../integration-services/service/ssis-catalog.md#Parameters)  
  
-   [Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor](../../integration-services/service/ssis-catalog.md#ServerEnvironments)  
  
-   [Execuções e validações](../../integration-services/service/ssis-catalog.md#Executions)  

##  <a name="CatalogObjectIdentifiers"></a> Identificadores de objetos do catálogo  
 Quando você cria um novo objeto no catálogo, atribua um nome ao objeto. O nome do objeto é um identificador. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define regras que estabelecem que os caracteres podem ser usados em um identificador. Os nomes destes objetos devem seguir as regras de identificador.  
  
-   Pasta  
  
-   Projeto  
  
-   Ambiente  
  
-   Parâmetro  
  
-   Variável de ambiente  
  
###  <a name="Folder"></a> Pasta, projeto e ambiente  
 Considere as seguintes regras ao renomear uma pasta, um projeto ou um ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), backspace (\b), null (\0) e tabulação (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   @ não é permitido como primeiro caractere, mas os caracteres subsequentes podem usar @.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
###  <a name="Parameter"></a> Parâmetro  
 Considere as seguintes regras ao nomear um parâmetro.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
###  <a name="EnvironmentVariable"></a> Variável de ambiente  
 Considere as seguintes regras ao nomear uma variável de ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), backspace (\b), null (\0) e tabulação (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   @ não é permitido como primeiro caractere, mas os caracteres subsequentes podem usar @.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
##  <a name="Configuration"></a> Configuração do catálogo  
 Você ajusta como o catálogo se comporta ajustando as propriedades do catálogo. As propriedades do catálogo definem como os dados confidenciais serão criptografados, e como as operações e os dados de controle de versão de projeto serão retidos. Para definir as propriedades do catálogo, use a caixa de diálogo **Propriedades do Catálogo** ou chame o procedimento armazenado [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md). Para exibir as propriedades, use a caixa de diálogo ou consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Acesse a caixa de diálogo clicando com o botão direito do mouse em **SSISDB** no Pesquisador de Objetos.  
  
###  <a name="Cleanup"></a> Operações e limpeza de versão do projeto  
 Os dados de status de muitas operações no catálogo são armazenados nas tabelas de banco de dados internas. Por exemplo, o catálogo rastreia o status das execuções de pacote e das implantações de projeto. Para manter o tamanho dos dados de operações, o **Trabalho de Manutenção do Servidor SSIS** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é usado para remover dados antigos. Este trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é criado quando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado.  
  
 Você pode atualizar ou reimplantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implantando-o com o mesmo nome na mesma pasta do catálogo. Por padrão, cada vez que você reimplanta um projeto, o catálogo **SSISDB** retém a versão anterior do projeto. Para manter o tamanho dos dados de operações, o **Trabalho de Manutenção do Servidor SSIS** é usado para remover versões antigas de projetos.  
 
Para executar o **Trabalho de Manutenção do Servidor SSIS**, o SSIS cria o logon do SQL Server **##MS_SSISServerCleanupJobLogin##**. Esse logon é apenas para uso interno do SSIS.
  
 As propriedades de catálogo **SSISDB** a seguir definem como este trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se comporta. Você pode exibir e modificar as propriedades usando a caixa de diálogo **Propriedades do Catálogo** ou usando [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) e [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 **Limpar Logs Periodicamente**  
 A etapa de trabalho para limpeza de operações é executada quando esta propriedade é definida como **True**.  
  
 **Período de Retenção (dias)**  
 Define a idade máxima dos dados de operações permitidos (em dias). Os dados mais antigos são removidos.  
  
 O valor mínimo é um dia. O valor máximo só é limitado pelo valor máximo dos dados **int** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre esse tipo de dados, consulte [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).  
  
 **Remover Periodicamente Versões Antigas**  
 A etapa de trabalho para limpeza de versão de projeto é executada quando esta propriedade é definida como **True**.  
  
 **Número Máximo de Versões por Projeto**  
 Define quantas versões de um projeto são armazenadas no catálogo. As versões de projetos mais antigas são removidas.  
  
###  <a name="Encryption"></a> Algoritmo de Criptografia  
 A propriedade **Algoritmo de Criptografia** especifica o tipo de criptografia usado para criptografar valores de parâmetro confidenciais. Você pode escolher entre os seguintes tipos de criptografia.  
  
-   AES_256 (padrão)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 Quando você implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o catálogo criptografará automaticamente os dados do pacote e os valores confidenciais. O catálogo também descriptografa automaticamente os dados quando você recupera-os. O catálogo SSISDB usa o nível de proteção **ServerStorage** . Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 Alterar o algoritmo de criptografia é uma operação demorada. Primeiro, o servidor tem que usar o algoritmo previamente especificado para descriptografar todos os valores de configuração. Em seguida, o servidor tem que usar o novo algoritmo para criptografar novamente os valores. Durante este momento, não pode haver outras operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor. Assim, para permitir que operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] continuem ininterruptas, o algoritmo de criptografia deverá ser um valor somente leitura na caixa de diálogo no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Para alterar a configuração da propriedade **Algoritmo de Criptografia** , defina o banco de dados **SSISDB** como modo de usuário único e chame o procedimento armazenado catalog.configure_catalog. Use ENCRYPTION_ALGORITHM para o argumento *property_name*. Para os valores de propriedade com suporte, consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Para obter mais informações sobre o procedimento armazenado, consulte [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 Para obter mais informações sobre o modo de usuário único, veja [Definir um banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md). Para obter informações sobre criptografia e algoritmos de criptografia no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte os tópicos na seção [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Uma chave mestra de banco de dados é usada para a criptografia. A chave é criada quando você cria o catálogo.  
  
 A tabela a seguir lista os nomes de propriedade mostrados na caixa de diálogo **Propriedades do Catálogo** e as propriedades correspondentes na exibição de banco de dados.  
  
|Nome da Propriedade (caixa de diálogo**Propriedades do Catálogo** )|Nome da Propriedade (exibição de banco de dados)|  
|---------------------------------------------------------|-------------------------------------|  
|Nome do Algoritmo de Criptografia|ENCRYPTION_ALGORITHM|  
|Limpar Logs Periodicamente|OPERATION_CLEANUP_ENABLED|  
|Período de Retenção (dias)|RETENTION_WINDOW|  
|Remover Periodicamente Versões Antigas|VERSION_CLEANUP_ENABLED|  
|Número Máximo de Versões por Projeto|MAX_PROJECT_VERSIONS|  
|Nível de Log Padrão em Todo o Servidor|SERVER_LOGGING_LEVEL|  
  
##  <a name="Permissions"></a> Permissões  
 Os projetos, ambientes e pacotes são armazenados em pastas, que são objetos protegíveis. Você pode conceder permissões a uma pasta, incluindo a permissão MANAGE_OBJECT_PERMISSIONS. MANAGE_OBJECT_PERMISSIONS permite delegar a administração do conteúdo da pasta a um usuário sem precisar conceder a associação do usuário à função ssis_admin. Você também pode conceder permissões para projetos, ambientes e operações. As operações incluem a inicialização do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a implantação de projetos, a criando e a inicialização de execuções, a validação de projetos e pacotes, e a configuração do catálogo **SSISDB** .  
  
 Para obter mais informações sobre as funções de banco de dados, veja [Funções no nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 O catálogo SSISDB usa um gatilho DDL, ddl_cleanup_object_permissions, para impor a integridade das informações de permissões para elementos protegíveis do SSIS. O gatilho é acionado quando uma entidade de segurança de banco de dados, como um usuário de banco de dados, função de banco de dados ou função de aplicativo de banco de dados, é removida do banco de dados SSISDB.  
  
 Se a entidade de segurança tiver concedido ou negado permissões a outras entidades de segurança, revogue as permissões dadas pelo concessor, para que a entidade de segurança possa ser removida. Caso contrário, uma mensagem de erro será retornada quando o sistema tentar remover a entidade de segurança. O gatilho removerá todos os registros de permissão em que a entidade de segurança de banco de dados é um usuário autorizado.  
  
 É recomendável que o gatilho não seja desabilitado porque ele assegura que não haverá nenhum registro de permissão órfão depois que uma entidade de segurança de banco de dados for removida do banco de dados **SSISDB** .  
  
### <a name="managing-permissions"></a>Gerenciando permissões  
 Você pode gerenciar permissões usando a interface do usuário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , procedimentos armazenados e o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> .  
  
 Para gerenciar permissões usando a interface de usuário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , use as seguintes caixas de diálogo:  
  
-   Para uma pasta, use a página **Permissões** da [Folder Properties Dialog Box](../../integration-services/service/folder-properties-dialog-box.md).  
  
-   Para um projeto, use a página **Permissões** na [Project Properties Dialog Box](../../integration-services/service/project-properties-dialog-box.md).  
  
-   Para um ambiente, use a página **Permissões** na [Caixa de Diálogo NIB: Propriedades do Ambiente](http://msdn.microsoft.com/en-us/6a91a8d4-0006-4cfd-9759-3e4295ae452b).  
  
 Para gerenciar permissões usando o Transact-SQL, chame [catalog.grant_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md), [catalog.deny_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md) e [catalog.revoke_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md). Para exibir permissões efetivas para a entidade de segurança atual para todos os objetos, consulte [catalog.effective_object_permissions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md). Este tópico fornece descrições dos diferentes tipos de permissões. Para exibir as permissões atribuídas explicitamente ao usuário, consulte [catalog.explicit_object_permissions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md).  
  
##  <a name="Folders"></a> Pastas  
 Uma pasta contém um ou mais projetos e ambientes no catálogo **SSISDB** . Você pode usar a exibição [catalog.folders &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md) para acessar informações sobre pastas no catálogo. Você pode usar os procedimentos armazenados a seguir para gerenciar pastas.  
  
-   [catalog.create_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="ProjectsAndPackages"></a> Projetos e pacotes  
 Cada projeto pode conter vários pacotes. Os projetos e pacotes podem conter parâmetros e referências a ambientes. Você pode acessar os parâmetros e referências de ambiente usando a [Configure Dialog Box](../../integration-services/service/configure-dialog-box.md).  
  
 Você pode executar outras tarefas de projeto chamando os seguintes procedimentos armazenados.  
  
-   [catalog.delete_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project &#40;&#40;Banco de dados SSISDB&#41;](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
  
-   [catalog.restore_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 Estas exibições fornecem detalhes sobre pacotes, projetos e versões de projeto.  
  
-   [catalog.projects &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="Parameters"></a> Parâmetros  
 Use os parâmetros para atribuir valores às propriedades de pacote no tempo de execução do pacote. Para definir o valor de um pacote ou parâmetro de projeto e limpar o valor, chame [catalog.set_object_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) e [catalog.clear_object_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md). Para definir o valor de um parâmetro para uma instância de execução, chame [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md). Você pode recuperar valores de parâmetro padrão chamando [catalog.get_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md).  
  
 Estas exibições mostram os parâmetros de todos os pacotes e projetos, e os valores de parâmetro usados para uma instância de execução.  
  
-   [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="ServerEnvironments"></a> Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor  
 Os ambientes de servidor contêm variáveis de servidor. Os valores variáveis podem ser usados quando um pacote é executado ou validado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os procedimentos armazenados a seguir permitem executar muitas outras tarefas de gerenciamento para ambientes e variáveis.  
  
-   [catalog.create_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
  
-   [catalog.delete_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
  
-   [catalog.move_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
  
-   [catalog.rename_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
  
-   [catalog.set_environment_property &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
  
-   [catalog.create_environment_variable &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
  
-   [catalog.delete_environment_variable &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_property &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
  
 Ao chamar o procedimento armazenado [catalog.set_environment_variable_protection &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md), você pode definir o bit de sensibilidade de uma variável.  
  
 Para usar o valor de uma variável de servidor, especifique a referência entre o projeto e o ambiente de servidor. Você pode usar os procedimentos armazenados para criar e excluir referências. Você também pode indicar se o ambiente pode estar localizado na mesma pasta que o projeto ou em uma pasta diferente.  
  
-   [catalog.create_environment_reference &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
  
-   [catalog.delete_environment_reference &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
  
-   [catalog.set_environment_reference_type &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
  
 Para obter mais detalhes sobre ambientes e variáveis, consulte estas exibições.  
  
-   [catalog.environments &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
  
-   [catalog.environment_variables &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
  
-   [catalog.environment_references &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
  
##  <a name="Executions"></a> Execuções e validações  
 Uma execução é uma instância de uma execução de pacote. Chame [catalog.create_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) e [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) para criar e iniciar uma execução. Para interromper a execução ou uma validação de pacote/projeto, chame [catalog.stop_operation &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md).  
  
 Para fazer com que um pacote em execução pause ou crie um arquivo de despejo, chame o procedimento armazenado catalog.create_execution_dump. Um arquivo de despejo fornece informações sobre a execução de um pacote que pode ajudar a solucionar problemas de execução. Para obter mais informações sobre como gerar e configurar arquivos de despejo, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 Para obter detalhes sobre execuções, validações, mensagens que são registradas em log durante operações, e informações contextuais relacionadas a erros, consulte estas exibições.  
  
-   [catalog.executions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
-   [catalog.operations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
  
-   [catalog.operation_messages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
  
-   [catalog.extended_operation_info &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
  
-   [catalog.event_messages](../../integration-services/system-views/catalog-event-messages.md)  
  
-   [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
 Você pode validar projetos e pacotes chamando os procedimentos armazenados [catalog.validate_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md) e [catalog.validate_package &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md). A exibição [catalog.validations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) fornece detalhes sobre validações, como as referências de ambiente de servidor consideradas na validação, se é uma validação de dependência ou uma validação completa e se o tempo de execução de 32 ou 64 bits é usado para executar o pacote.  

## <a name="create-the-ssis-catalog"></a>Criar o catálogo SSIS
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes em um servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para poder implantar os projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o servidor deve conter o catálogo do **SSISDB** . O programa de instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] não cria o catálogo automaticamente; você precisará criar o catálogo manualmente por meio das instruções a seguir.  
  
 Você pode criar o catálogo do SSISDB no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode criar o catálogo programaticamente usando o Windows PowerShell.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>Para criar o catálogo SSISDB no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Conecte-se ao Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  No Pesquisador de Objetos, expanda o nó de servidor, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Criar Catálogo**.  
  
4.  Clique em **Habilitar Integração CLR**.  
  
     Esse catálogo usa procedimentos armazenados CLR.  
  
5.  Clique em **Habilitar a execução automática de procedimento armazenado do Integration Services na inicialização do SQL Server** para habilitar o procedimento armazenado [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md) a ser executado toda vez que a instância do servidor [!INCLUDE[ssIS](../../includes/ssis-md.md)] for reiniciada.  
  
     O procedimento armazenado executa a manutenção do estado das operações para o catálogo SSISDB. Ele corrigirá o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor [!INCLUDE[ssIS](../../includes/ssis-md.md)] ficar inoperante.  
  
6.  Digite uma senha e clique em **Ok**.  
  
     A senha protege a chave mestra do banco de dados que é usada para criptografar os dados do catálogo. Salve a senha em um local seguro. É recomendado que você também faça backup da chave mestra do banco de dados. Para obter mais informações, consulte [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>Para criar o catálogo do SSISDB programaticamente  
  
1.  Execute o seguinte script do PowerShell:  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     Para obter mais exemplos de como usar o Windows PowerShell e o <xref:Microsoft.SqlServer.Management.IntegrationServices> namespace, consulte a entrada de blog, [SSIS e PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539), em blogs.msdn.com. Para obter uma visão geral do namespace e dos exemplos de códigos, consulte a entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=254267)em blogs.msdn.com.  

## <a name="catalog-properties-dialog-box"></a>Caixa de diálogo Propriedades do Catálogo
  Use a caixa de diálogo de Propriedades do Catálogo para configurar o catálogo do SSISDB. As propriedades do catálogo definem como dados confidenciais são criptografados, como dados de operações e de controle de versão de projeto são retidos, e quando o tempo limite de operações de validação expira. O catálogo do SSISDB é um armazenamento e ponto de administração central para projetos, pacotes, parâmetros e ambientes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Você também pode exibir propriedades do catálogo na exibição catalog.catalog_property e definir propriedades por meio do procedimento armazenado catalog.configure_catalog. Para obter mais informações, consulte [catalog.catalog_properties &#40;banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) e [catalog.configure_catalog &#40;banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Propriedades do Catálogo](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
###  <a name="open_dialog"></a> Abrir a caixa de diálogo Propriedades do Catálogo  
  
1.  Abra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Conecte-se ao Mecanismo de Banco de Dados do Microsoft SQL Server.  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services** , clique com o botão direito do mouse em **SSISDB**e clique em **Propriedades**.  
  
###  <a name="options"></a> Configurar as opções  
  
#### <a name="options"></a>Opções  
 A tabela a seguir descreve determinadas propriedades na caixa de diálogo e as propriedades correspondentes na exibição de catalog.catalog_property.  
  
|Nome da Propriedade (caixa de diálogo Propriedades do Catálogo)|Nome da Propriedade (exibição catalog.catalog_property)|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|Nome do Algoritmo de Criptografia|ENCRYPTION_CLEANUP_ENABLED|Especifica o tipo de criptografia usado para criptografar os valores dos parâmetros confidenciais no catálogo. O valores possíveis são os seguintes:<br /><br /> DES<br /><br /> TRIPLE_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESPX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256 (padrão)|  
|Tempo Limite de Validação (segundos)|VALIDATION_TIMEOUT|Especifique o número máximo de segundos que a validação de um projeto ou de um pacote pode ser executada antes de ser parada. O valor padrão é 300 segundos.<br /><br /> A execução da validação é uma operação assíncrona. Quanto maior for o projeto ou o pacote, mais tempo será necessário para a validação.<br /><br /> Para obter informações sobre como validar projetos e pacotes, consulte [Tipos de dados do Integration Services em expressões](../../integration-services/expressions/integration-services-data-types-in-expressions.md).|  
|Limpar Logs Periodicamente|OPERATION_CLEANUP_ENABLED|Defina a propriedade como True para indicar que o trabalho do SQL Server Agent, limpeza de operações, é executada. Caso contrário, defina a propriedade como False.|  
|Período de Retenção (dias)|RETENTION_WINDOW|Especifique a idade máxima dos dados de operações permitidos (em dias). Dados mais antigos do que o número de dias especificado serão removidos pelo trabalho do SQL Agent, limpeza de operações.|  
|Número Máximo de Versões por Projeto|MAX_PROJECT_VERSIONS|Especifique quantas versões de um projeto serão armazenadas no catálogo. Versões de projetos mais antigas que excederem o número máximo serão removidas quando o trabalho de limpeza de versões do projeto for executado.|  

## <a name="back-up-restore-and-move-the-ssis-catalog"></a>Fazer backup, restaurar e mover o catálogo do SSIS
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] inclui o banco de dados SSISDB. Você consulta exibições no banco de dados SSISDB para inspecionar objetos, configurações e dados operacionais que são armazenados no catálogo do **SSISDB** . Este tópico fornece instruções para fazer backup do banco de dados e restaurá-lo.  
  
 O catálogo do **SSISDB** armazena os pacotes que você implantou no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre o catálogo, consulte [Catálogo do SSIS](../../integration-services/service/ssis-catalog.md).  
  
###  <a name="backup"></a> Para fazer o backup do banco de dados SSIS  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Faça backup da chave mestra para o banco de dados do SSISDB, usando a instrução Transact-SQL BACKUP MASTER KEY. A chave é armazenada em um arquivo que você especifica. Use a senha para criptografar a chave mestra no arquivo.  
  
     Para obter mais informações sobre a instrução, consulte [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md).  
  
     No exemplo a seguir, a chave mestra é exportada para o arquivo `c:\temp directory\RCTestInstKey`. A senha `LS2Setup!` é usada para criptografar a chave mestra.  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  Faça backup do banco de dados do SSISDB usando a caixa de diálogo **Backup de Banco de Dados** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Como fazer backup de um banco de dados (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=231812).  
  
4.  Gere o script de CREATE LOGIN para ##MS_SSISServerCleanupJobLogin ##, fazendo o seguinte. Para obter mais informações, veja [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md).  
  
    1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó **Segurança** e expanda o nó **Logons**.  
  
    2.  Clique com o botão direito do mouse em **##MS_SSISServerCleanupJobLogin##**e clique em **Script de Logon como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
5.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB nunca foi criado, gere o script CREATE PROCEDURE para sp_ssis_startup, fazendo o seguinte. Para obter mais informações, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
    1.  No Pesquisador de Objetos, expanda o nó **Bancos de Dados** e, em seguida, expanda o nó **mestre** > **Programação** > **Procedimentos Armazenados**.  
  
    2.  Clique com o botão direito do mouse em **dbo.sp_ssis_startup**e clique em **Script de Procedimento Armazenado como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
6.  Confirme que o SQL Server Agent foi iniciado  
  
7.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB nunca foi criado, gere um script para o Trabalho de Manutenção do Servidor SSIS, fazendo o seguinte. O script é criado automaticamente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando o catálogo do SSISDB é criado. O trabalho ajuda a limpar os logs da operação de limpeza fora da janela de retenção e remove versões anteriores de projetos.  
  
    1.  No Pesquisador de Objetos, expanda o nó **SQL Server Agent** e, em seguida, expanda o nó **Trabalhos** .  
  
    2.  Clique com o botão direito do mouse em Trabalho de Manutenção do Servidor SSIS e clique em **Script de Trabalho como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
### <a name="to-restore-the-ssis-database"></a>Para restaurar o banco de dados SSIS  
  
1.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o catálogo do SSISDB nunca foi criado, habilite o clr (Common Language Runtime) executando o procedimento armazenado sp_configure. Para obter mais informações, veja [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e [Opção clr habilitado](http://go.microsoft.com/fwlink/?LinkId=231855).  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o catálogo do SSISDB nunca foi criado, crie a chave assimétrica e o logon da chave assimétrica e conceda permissão UNSAFE para o logon.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Os procedimentos armazenados CLR exigem que permissões de UNSAFE sejam concedidas ao logon porque o logon exige acesso adicional a recursos restritos, como a API do Microsoft Win32. Para obter mais informações sobre a permissão de código UNSAFE, consulte [Criando um assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  Restaure o banco de dados SSISDB do backup usando a caixa de diálogo **Restaurar Banco de Dados** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte os tópicos a seguir.  
  
    -   [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
    -   [Restaurar banco de dados &#40;página Arquivos&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [Restaurar banco de dados &#40;página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  Execute os scripts que você criou no procedimento [Para fazer backup do banco de dados SSIS](#backup) para ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup e Trabalho de Manutenção do Servidor SSIS. Confirme que o SQL Server Agent foi iniciado.  
  
5.  Execute a instrução a seguir para definir o procedimento sp_ssis_startup para execução automática. Para obter mais informações, veja [sp_procoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md).  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  Mapeie o usuário do SSISDB ##MS_SSISServerCleanupJobUser## (banco de dados do SSISDB) para ##MS_SSISServerCleanupJobLogin## usando a caixa de diálogo **Propriedades de Logon** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
7.  Restaure a chave mestra usando um dos seguintes métodos. Para obter mais informações sobre criptografia, consulte [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
    -   **Método 1**  
  
         Use este método se você já executou um backup da chave mestra do banco de dados e você tem a senha usada para criptografar a chave mestra.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  Confirme que a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões para ler o arquivo da chave de backup.  
  
        > [!NOTE]  
        >  Você verá a seguinte mensagem de aviso exibida no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se a chave mestra de banco de dados ainda não tiver sido criptografada pela chave mestra de serviço. Ignore a mensagem de aviso.  
        >   
        >  **A chave mestra atual não pode ser descriptografada. O erro foi ignorado porque a opção FORCE foi especificada.**  
        >   
        >  O argumento FORCE especifica que o processo de restauração deve continuar mesmo se a chave mestra de banco de dados atual não estiver aberta. Para o catálogo do SSISDB, como a chave mestra de banco de dados não foi aberta na instância onde você está restaurando o banco de dados, você verá esta mensagem.  
  
    -   **Método 2**  
  
         Use este método se você tiver a senha original que foi usada para criar o SSISDB.  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  Determine se o esquema de catálogo SSISDB e os binários [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ISServerExec e SQLCLR assembly) são compatíveis executando [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md).  
  
9. Para confirmar que o banco de dados do SSISDB foi restaurado com êxito, execute operações no catálogo d SSISDB, por exemplo, executar pacotes que foram implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [pacotes executar Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md).  
  
### <a name="to-move-the-ssis-database"></a>Para mover o banco de dados SSIS  
  
-   Siga as instruções para mover bancos de dados de usuários. Para obter mais informações, veja [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md).  
  
     Assegure-se de fazer backup da chave mestra do banco de dados SSISDB e proteger o arquivo de backup. Para obter mais informações, consulte [Para fazer o backup do banco de dados SSIS](#backup).  
  
     Verifique se os objetos pertinentes do Integration Services (SSIS) estão criados na nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB ainda não foi criado.  

## <a name="upgrade-the-ssis-catalog-ssisdb"></a>Atualizar o Catálogo SSIS (SSISDB)
  Execute o Assistente de atualização do SSISDB para atualizar o banco de dados do catálogo do SSIS, SSISDB, quando o banco de dados for mais antigo que a versão atual da instância do SQL Server. Isso ocorre quando uma das condições a seguir é verdadeira.  
  
-   Você restaurou o banco de dados de uma versão anterior do SQL Server.  
  
-   Você não removeu o banco de dados de um Grupo de Disponibilidade AlwaysOn antes de atualizar a instância do SQL Server. Isso impede a atualização automática do banco de dados. Para obter mais informações, consulte [Upgrading SSISDB in an availability group](#Upgrade).  
  
 O assistente só pode atualizar o banco de dados em uma instância de servidor local.  
  
### <a name="upgrade-the-ssis-catalog-ssisdb-by-running-the-ssisdb-upgrade-wizard"></a>Atualizar o Catálogo SSIS (SSISDB) executando o Assistente de Atualização do SSISDB  
  
1.  Fazer backup do banco de dados do Catálogo SSIS, SSISDB.  
  
2.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o servidor local e expanda **Catálogos do Integration Services**.  
  
3.  Clique com o botão direito do mouse em **SSISDB**e selecione **Atualização do Banco de Dados** para iniciar o Assistente de Atualização do SSISDB.  
  
     ![Iniciar o Assistente de atualização do SSISDB](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "iniciar o Assistente de atualização do SSISDB")  
  
4.  Na página **Selecionar Instância** , escolha uma instância do SQL Server no servidor local.  
  
    > [!IMPORTANT]  
    >  O assistente só pode atualizar o banco de dados em uma instância de servidor local.  
  
     Marque a caixa de seleção para indicar que você fez backup do banco de dados SSISDB antes de executar o assistente.  
  
     ![Selecione o servidor no Assistente de atualização do SSISDB](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "selecione o servidor no Assistente de atualização do SSISDB")  
  
5.  Escolha **Atualizar** para atualizar o banco de dados do Catálogo SSIS.  
  
6.  Na página **Resultado** , examine os resultados.  
  
     ![Examine os resultados do Assistente de atualização do SSISDB](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "revisar os resultados do Assistente de atualização do SSISDB")  

## <a name="always-on-for-ssis-catalog-ssisdb"></a>AlwaysOn para catálogo do SSIS (SSISDB)
  O recurso Grupos de Disponibilidade AlwaysOn é uma solução de alta disponibilidade e recuperação de desastres que fornece uma alternativa de nível corporativo para espelhamento de banco de dados. Um grupo de disponibilidade permite um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como bancos de dados de disponibilidade, que fazem failover juntos. Para obter mais informações, confira [Grupos de Disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).  
  
 Para fornecer a alta disponibilidade ao catálogo do SSIS (SSISDB) e seu conteúdo (projetos, pacotes, logs de execução, etc.), você pode adicionar o banco de dados do SSISDB (da mesma forma que qualquer outro banco de dados de usuário) a um Grupo de Disponibilidade AlwaysOn. Quando ocorre um failover, um dos nós secundários automaticamente se torna o novo nó primário.  
 
 > [!IMPORTANT]
 > Quando ocorre um failover, os pacotes que estavam em execução não reiniciam ou retomam. 
 
 **Nesta seção:**  
  
1.  [Pré-requisitos](#prereq)  
  
2.  [Configurar o suporte do SSIS para Always On](#Firsttime)  
  
3.  [Atualizando o SSISDB em um grupo de disponibilidade](#Upgrade)  
  
###  <a name="prereq"></a> Pré-requisitos  
 Você deve executar as seguintes etapas de pré-requisito antes de habilitar o suporte do Always On para o banco de dados do SSISDB.  
  
1.  Configurar um cluster de failover do Windows. Confira a postagem do blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalando o recurso Cluster de Failover e as Ferramentas para o Windows Server 2012) para obter instruções. Você deve instalar o recurso e as ferramentas em todos os nós de cluster.  
  
2.  Instalar o recurso SSIS (SQL Server 2016 com Integration Services) em cada nó do cluster.  
  
3.  Habilite grupos de disponibilidade AlwaysOn para cada instância do SQL Server. Confira [Habilitar Grupos de Disponibilidade Always On](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md) para obter detalhes.  
  
###  <a name="Firsttime"></a> Configurar o suporte do SSIS para Always On  
  
-   [Etapa 1: Criar o catálogo do Integration Services](#Step1)  
  
-   [Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On](#Step2)  
  
-   [Etapa 3: Habilitar o suporte do SSIS para o Always On](#Step3)  
  
> [!IMPORTANT]  
> -   Você deve executar estas etapas no **nó primário** do grupo de disponibilidade.
> -   Você deve habilitar **suporte do SSIS para AlwaysOn** *depois* adicionar o SSISDB a um grupo de disponibilidade AlwaysOn.  
  
####  <a name="Step1"></a> Etapa 1: Criar o catálogo do Integration Services  
  
1.  Inicie o **SQL Server Management Studio** e o conecte a uma instância do SQL Server no cluster que você deseja definir como o **nó primário** do grupo de alta disponibilidade do Always On para SSISDB.  
  
2.  No Pesquisador de Objetos, expanda o nó de servidor, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Criar Catálogo**.  
  
3.  Clique em **Habilitar Integração CLR**. Esse catálogo usa procedimentos armazenados CLR.  
  
4.  Clique em **Habilitar a execução automática de procedimento armazenado do Integration Services na inicialização do SQL Server** para habilitar o procedimento armazenado [catalog.startup](../system-stored-procedures/catalog-startup.md) a ser executado toda vez que a instância do servidor SSIS for reiniciada. O procedimento armazenado executa a manutenção do estado das operações para o catálogo SSISDB. Ele corrigirá o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor SSIS ficar inoperante.  
  
5.  Digite uma **senha**e clique em **OK**. A senha protege a chave mestra do banco de dados que é usada para criptografar os dados do catálogo. Salve a senha em um local seguro. É recomendado que você também faça backup da chave mestra do banco de dados. Para obter mais informações, consulte [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
####  <a name="Step2"></a> Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On  
 Adicionar o banco de dados do SSISDB a um Grupo de Disponibilidade Always On é quase igual a adicionar qualquer outro banco de dados de usuário em um grupo de disponibilidade. Confira [Use the Availability Group Wizard](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)(Usar o assistente do Grupo de Disponibilidade).  
  
 Você precisa fornecer a senha que especificou ao criar o Catálogo do SSIS na página **Selecionar Bancos de Dados** do assistente **Novo Grupo de Disponibilidade** .  
  
 ![Novo Grupo de Disponibilidade](../../integration-services/service/media/ssis-newavailabilitygroup.png "Novo Grupo de Disponibilidade")  
  
####  <a name="Step3"></a> Etapa 3: Habilitar o suporte do SSIS para o Always On  
 Depois de criar o Catálogo do Integration Services, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Habilitar Suporte do Always On...**. Você deve ver a seguinte caixa de diálogo **Habilitar Suporte para Always On** . Se esse item de menu estiver desabilitado, verifique se você tem todos os pré-requisitos instalados e clique em **Atualizar**.  
  
 ![Habilitar o suporte para sempre](../../integration-services/service/media/ssis-enablesupportforalwayson.png)  
  
> [!WARNING]  
>  O failover automático do banco de dados do SSISDB só será permitido quando você habilitar o Suporte do SSIS para o Always On.  
  
 As réplicas secundárias recentemente adicionadas do grupo de disponibilidade AlwaysOn aparecerá na tabela. Clique em **Conectar …** de cada réplica na lista e digite as credenciais de autenticação para se conectar à réplica. A conta de usuário deve ser um membro do grupo sysadmin em cada réplica para habilitar o suporte do SSIS para AlwaysOn. Depois de se conectar com êxito a cada réplica, clique em **OK** para habilitar o suporte do SSIS para Always On.  
 
Se o **habilitar o suporte AlwaysOn no** opção no menu de contexto parece estar desabilitada depois de concluir os pré-requisitos, tente estas coisas:
1.  Atualizar o menu de contexto clicando o **atualização** opção.
2.  Verifique se que você está se conectando ao nó principal. Você precisa habilitar o suporte AlwaysOn no nó primário.
3.  Verifique se que a versão do SQL Server é 13.0 ou superior. O SSIS dá suporte a AlwaysOn apenas no SQL Server 2016 e versões posteriores.

###  <a name="Upgrade"></a> Atualizando o SSISDB em um grupo de disponibilidade  
 Se estiver atualizando o SQL Server de uma versão anterior, e o SSISDB estiver em um grupo de disponibilidade Always On, sua atualização poderá ser bloqueada pela regra "Verificação do SSISDB no Grupo de Disponibilidade Always On". Esse bloqueio ocorre porque a atualização é executada no modo de usuário único, enquanto um banco de dados de disponibilidade deve ser um banco de dados de multiusuário. Portanto, durante a atualização ou a aplicação de patch, todos os bancos de dados de disponibilidade, incluindo o SSISDB, são colocados no modo offline e não são atualizados nem corrigidos. Para que a atualização continue, você precisa remover o SSISDB do grupo de disponibilidade, atualizar ou corrigir cada nó e adicionar o SSISDB de volta ao grupo de disponibilidade.  
  
 Se você estiver bloqueado pela regra "Verificação do SSISDB no Grupo de Disponibilidade Always On", será preciso seguir estas etapas para atualizar o SQL Server.  
  
1.  Remova o banco de dados do SSISDB do grupo de disponibilidade. Para obter mais informações, veja [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) e [Remover um banco de dados primário de um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
2.  Clique em **Executar novamente** no assistente de atualização. A regra "Verificação do SSISDB no Grupo de Disponibilidade Always On" passará.  
  
3.  Clique em **Avançar** para continuar a atualização.  
  
4.  Depois de atualizar todos os nós, adicione o banco de dados do SSISDB de volta ao grupo de disponibilidade Always On. Para obter mais informações, consulte [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/availability-group-add-a-database.md).  
  
 Se você não estiver bloqueado ao fazer a atualização do SQL Server, e o SSISDB estiver em um grupo de disponibilidade Always On, será preciso fazer a atualização do SSISDB separadamente depois de fazer a atualização do mecanismo de banco de dados do SQL Server. Use o Assistente de Atualização do SSIS para atualizar o SSISDB, conforme descrito no procedimento a seguir.  
  
1.  Mova o banco de dados do SSISDB para fora do grupo de disponibilidade ou exclua o grupo de disponibilidade se o SSISDB for o único banco de dados no grupo de disponibilidade. Você precisa iniciar o **SQL Server Management Studio** no **nó primário** do grupo de disponibilidade para executar essa tarefa.  
  
2.  Remova o banco de dados do SSISDB de todos os **nós de réplica**.  
  
3.  Atualize o banco de dados do SSISDB no **nó primário**. No**Pesquisador de Objetos** do SQL Server Management Studio, expanda **Catálogos do Integration Services**, clique com o botão direito do mouse em **SSISDB**e selecione **Atualização do Banco de Dados**. Siga as instruções do **Assistente de Atualização do SSISDB** para atualizar o banco de dados. Você precisa iniciar o **Assistente de Atualização do SSISDB** localmente no **nó primário**.  
  
4.  Siga as instruções em [Etapa 2: Adicionar o SSISDB a um Grupo de Disponibilidade Always On](#Step2) para adicionar o SSISDB a um grupo de disponibilidade.  
  
5.  Siga as instruções em [Etapa 3: Habilitar o suporte do SSIS para o Always On](#Step3).  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   Entrada de blog, [SSIS e PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539), em blogs.msdn.com.  
  
-   Entrada de blog, [Digas de controle de acesso ao catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=246669), em blogs.msdn.com.  
  
-   Entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=254267)em blogs.msdn.com.  

