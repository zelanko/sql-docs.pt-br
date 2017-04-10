---
title: "Cat&#225;logo do SSIS | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Cat&#225;logo do SSIS
  O catálogo do **SSISDB** é o ponto central para trabalhar com projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) que você implantou no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por exemplo, você define parâmetros de projeto e pacote, configura ambientes para especificar valores de tempo de execução para pacotes, executa e soluciona problemas de pacotes, e gerencia as operações de servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os objetos armazenados no catálogo **SSISDB** incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 Você inspeciona objetos, configurações e dados operacionais que são armazenados no catálogo do **SSISDB** , consultando as exibições no banco de dados **SSISDB** . Você gerencia os objetos chamando procedimentos armazenados no banco de dados **SSISDB** ou usando a interface de usuário do catálogo **SSISDB** . Em muitos casos, a mesma tarefa pode ser executada na interface de usuário ou chamando um procedimento armazenado.  
  
 Para manter o banco de dados **SSISDB** , é recomendado que você aplique políticas empresariais padrão para gerenciar os bancos de dados de usuários. Para obter informações sobre como criar planos de manutenção, consulte [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md).  
  
 O catálogo **SSISDB** e o banco de dados **SSISDB** dão suporte ao Windows PowerShell. Para obter mais informações sobre como usar o SQL Server com Windows PowerShell, consulte [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md). Para obter exemplos de como usar o Windows PowerShell para concluir tarefas como implantar um projeto, consultar a entrada de blog, [SSIS e PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539)em blogs.msdn.com.  
  
 Para obter mais informações sobre como exibir dados de operações, consulte [Monitorar pacote em execução e outras operações](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
 Você acessa o catálogo **SSISDB** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conectando-se ao Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e expandindo o nó **Catálogos do Integration Services** no Pesquisador de Objetos. Você acessa o banco de dados **SSISDB** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] expandindo o nó Bancos de Dados no Pesquisador de Objetos.  
  
> [!NOTE] Não é possível renomear o banco de dados **SSISDB** .  
  
> [!NOTE] Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual o banco de dados **SSISDB** está anexado para ou não responde, o processo ISServerExec.exe termina. Uma mensagem é gravada em um log de Eventos do Windows.  
>   
>  Se os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizarem failover como parte de um failover de cluster, os pacotes de execução não serão reiniciados. Você pode usar pontos de verificação para reiniciar pacotes. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="in-this-topic"></a>Neste tópico  
  
-   [Identificadores de objetos do catálogo](../../integration-services/service/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [Configuração do catálogo](../../integration-services/service/ssis-catalog.md#Configuration)  
  
-   [Permissões](../../integration-services/service/ssis-catalog.md#Permissions)  
  
-   [Pastas](../../integration-services/service/ssis-catalog.md#Folders)  
  
-   [Projetos e pacotes](../../integration-services/service/ssis-catalog.md#ProjectsAndPackages)  
  
-   [Parâmetros](../../integration-services/service/ssis-catalog.md#Parameters)  
  
-   [Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor](../../integration-services/service/ssis-catalog.md#ServerEnvironments)  
  
-   [Execuções e validações](../../integration-services/service/ssis-catalog.md#Executions)  
  
-   [Suporte a AlwaysOn](../../integration-services/service/ssis-catalog.md#AlwaysOn)  
  
-   [Tarefas relacionadas](../../integration-services/service/ssis-catalog.md#RelatedTasks)  
  
-   [Conteúdo relacionado](../../integration-services/service/ssis-catalog.md#RelatedContent)  
  
##  <a name="a-namecatalogobjectidentifiersa-catalog-object-identifiers"></a><a name="CatalogObjectIdentifiers"></a> Identificadores de objetos do catálogo  
 Quando você cria um novo objeto no catálogo, atribua um nome ao objeto. O nome do objeto é um identificador. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define regras que estabelecem que os caracteres podem ser usados em um identificador. Os nomes destes objetos devem seguir as regras de identificador.  
  
-   Pasta  
  
-   Projeto  
  
-   Ambiente  
  
-   Parâmetro  
  
-   Variável de ambiente  
  
###  <a name="a-namefoldera-folder-project-environment"></a><a name="Folder"></a> Pasta, projeto e ambiente  
 Considere as seguintes regras ao renomear uma pasta, um projeto ou um ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), retrocesso (\b), nulo (\0) e tabulação (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   @ não é permitido como o primeiro caractere, mas os caracteres subsequentes podem usar @.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
###  <a name="a-nameparametera-parameter"></a><a name="Parameter"></a> Parâmetro  
 Considere as seguintes regras ao nomear um parâmetro.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
###  <a name="a-nameenvironmentvariablea-environment-variable"></a><a name="EnvironmentVariable"></a> Variável de ambiente  
 Considere as seguintes regras ao nomear uma variável de ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), retrocesso (\b), nulo (\0) e tabulação (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   @ não é permitido como o primeiro caractere, mas os caracteres subsequentes podem usar @.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
##  <a name="a-nameconfigurationa-catalog-configuration"></a><a name="Configuration"></a> Configuração do catálogo  
 Você ajusta como o catálogo se comporta ajustando as propriedades do catálogo. As propriedades do catálogo definem como os dados confidenciais serão criptografados, e como as operações e os dados de controle de versão de projeto serão retidos. Para definir as propriedades do catálogo, use a caixa de diálogo **Propriedades do Catálogo** ou chame o procedimento armazenado [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md). Para exibir as propriedades, use a caixa de diálogo ou consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Acesse a caixa de diálogo clicando com o botão direito do mouse em **SSISDB** no Pesquisador de Objetos.  
  
###  <a name="a-namecleanupa-operations-and-project-version-cleanup"></a><a name="Cleanup"></a> Operações e limpeza de versão do projeto  
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
  
###  <a name="a-nameencryptiona-encryption-algorithm"></a><a name="Encryption"></a> Algoritmo de Criptografia  
 A propriedade **Algoritmo de Criptografia** especifica o tipo de criptografia usado para criptografar valores de parâmetro confidenciais. Você pode escolher entre os seguintes tipos de criptografia.  
  
-   AES_256 (padrão)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 Quando você implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o catálogo criptografará automaticamente os dados do pacote e os valores confidenciais. O catálogo também descriptografa automaticamente os dados quando você recupera-os. O catálogo SSISDB usa o nível de proteção **ServerStorage** . Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 Alterar o algoritmo de criptografia é uma operação demorada. Primeiro, o servidor tem que usar o algoritmo previamente especificado para descriptografar todos os valores de configuração. Em seguida, o servidor tem que usar o novo algoritmo para criptografar novamente os valores. Durante este momento, não pode haver outras operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor. Assim, para permitir que operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] continuem ininterruptas, o algoritmo de criptografia deverá ser um valor somente leitura na caixa de diálogo no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Para alterar a configuração da propriedade **Algoritmo de Criptografia** , defina o banco de dados **SSISDB** como modo de usuário único e chame o procedimento armazenado catalog.configure_catalog. Use ENCRYPTION_ALGORITHM para o argumento *property_name*. Para os valores de propriedade com suporte, consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Para obter mais informações sobre o procedimento armazenado, consulte [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 Para obter mais informações sobre o modo de usuário único, veja [Definir um banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md). Para obter informações sobre criptografia e algoritmos de criptografia no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte os tópicos na seção [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Uma chave mestra de banco de dados é usada para a criptografia. A chave é criada quando você cria o catálogo. Para obter mais informações, consulte [Criar o catálogo SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
 A tabela a seguir lista os nomes de propriedade mostrados na caixa de diálogo **Propriedades do Catálogo** e as propriedades correspondentes na exibição de banco de dados.  
  
|Nome da Propriedade (caixa de diálogo**Propriedades do Catálogo** )|Nome da Propriedade (exibição de banco de dados)|  
|---------------------------------------------------------|-------------------------------------|  
|Nome do Algoritmo de Criptografia|ENCRYPTION_ALGORITHM|  
|Limpar Logs Periodicamente|OPERATION_CLEANUP_ENABLED|  
|Período de Retenção (dias)|RETENTION_WINDOW|  
|Remover Periodicamente Versões Antigas|VERSION_CLEANUP_ENABLED|  
|Número Máximo de Versões por Projeto|MAX_PROJECT_VERSIONS|  
|Nível de Log Padrão em Todo o Servidor|SERVER_LOGGING_LEVEL|  
  
##  <a name="a-namepermissionsa-permissions"></a><a name="Permissions"></a> Permissões  
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
  
-   Para um ambiente, use a página **Permissões** na [Caixa de Diálogo NIB: Propriedades do Ambiente](http://msdn.microsoft.com/pt-br/6a91a8d4-0006-4cfd-9759-3e4295ae452b).  
  
 Para gerenciar permissões usando o Transact-SQL, chame [catalog.grant_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md), [catalog.deny_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md) e [catalog.revoke_permission &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md). Para exibir permissões efetivas para a entidade de segurança atual para todos os objetos, consulte [catalog.effective_object_permissions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md). Este tópico fornece descrições dos diferentes tipos de permissões. Para exibir as permissões atribuídas explicitamente ao usuário, consulte [catalog.explicit_object_permissions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md).  
  
##  <a name="a-namefoldersa-folders"></a><a name="Folders"></a> Pastas  
 Uma pasta contém um ou mais projetos e ambientes no catálogo **SSISDB** . Você pode usar a exibição [catalog.folders &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md) para acessar informações sobre pastas no catálogo. Você pode usar os procedimentos armazenados a seguir para gerenciar pastas.  
  
-   [catalog.create_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="a-nameprojectsandpackagesa-projects-and-packages"></a><a name="ProjectsAndPackages"></a> Projetos e pacotes  
 Cada projeto pode conter vários pacotes. Os projetos e pacotes podem conter parâmetros e referências a ambientes. Você pode acessar os parâmetros e referências de ambiente usando a [Configure Dialog Box](../../integration-services/service/configure-dialog-box.md).  
  
 Você pode executar outras tarefas de projeto chamando os seguintes procedimentos armazenados.  
  
-   [catalog.delete_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project &#40;&#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
  
-   [catalog.restore_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 Estas exibições fornecem detalhes sobre pacotes, projetos e versões de projeto.  
  
-   [catalog.projects &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="a-nameparametersa-parameters"></a><a name="Parameters"></a> Parâmetros  
 Use os parâmetros para atribuir valores às propriedades de pacote no tempo de execução do pacote. Para definir o valor de um pacote ou parâmetro de projeto e limpar o valor, chame [catalog.set_object_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) e [catalog.clear_object_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md). Para definir o valor de um parâmetro para uma instância de execução, chame [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md). Você pode recuperar valores de parâmetro padrão chamando [catalog.get_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md).  
  
 Estas exibições mostram os parâmetros de todos os pacotes e projetos, e os valores de parâmetro usados para uma instância de execução.  
  
-   [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="a-nameserverenvironmentsa-server-environments-server-variables-and-server-environment-references"></a><a name="ServerEnvironments"></a> Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor  
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
  
##  <a name="a-nameexecutionsa-executions-and-validations"></a><a name="Executions"></a> Execuções e validações  
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
  
##  <a name="a-namealwaysona-alwayson-support"></a><a name="AlwaysOn"></a> Suporte a AlwaysOn  
 O recurso Grupos de Disponibilidade AlwaysOn é uma solução de alta disponibilidade e recuperação de desastres que fornece uma alternativa de nível corporativo para espelhamento de banco de dados. Um grupo de disponibilidade dá suporte a um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como bancos de dados de disponibilidade, que fazem failover juntos. Para saber mais, confira [Grupos de Disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o SSIS (SQL Server Integration Services) introduz novas funcionalidades que permitem uma fácil implantação em um Catálogo do SSIS centralizado (ou seja, banco de dados de usuário SSISDB). Para fornecer a alta disponibilidade ao banco de dados do SSISDB e seu conteúdo (projetos, pacotes, logs de execução etc.), você pode adicionar o banco de dados do SSISDB (da mesma forma que qualquer outro banco de dados de usuário) a um Grupo de Disponibilidade AlwaysOn. Quando ocorre um failover, um dos nós secundários automaticamente se torna o novo nó primário.  
  
 Para obter uma visão geral detalhada e instruções passo a passo para habilitar o AlwaysOn para SSISDB, consulte [AlwaysOn para Catálogo do SSIS &#40;SSISDB&#41;](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md).  
  
##  <a name="a-namerelatedtasksa-related-tasks"></a><a name="RelatedTasks"></a> Tarefas Relacionadas  
  
-   [Criar o catálogo do SSIS](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Fazer backup, restaurar e mover o catálogo do SSIS](../../integration-services/service/backup-restore-and-move-the-ssis-catalog.md)  
  
##  <a name="a-namerelatedcontenta-related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   Entrada de blog, [SSIS e PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539), em blogs.msdn.com.  
  
-   Entrada de blog, [Digas de controle de acesso ao catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=246669), em blogs.msdn.com.  
  
-   Entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=254267)em blogs.msdn.com.  
  
  