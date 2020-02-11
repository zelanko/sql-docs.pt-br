---
title: sp_addmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: a296f5b4cb20768d5aa244646e584bede110d26a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72278356"
---
# <a name="sp_addmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria uma nova publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados que está sendo publicado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação de mesclagem a ser criada. a *publicação* é **sysname**, sem padrão, e não deve ser a palavra-chave ALL. O nome da publicação deve ser exclusivo no banco de dados.  
  
`[ @description = ] 'description'`É a descrição da publicação. a *Descrição* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @retention = ] retention`É o período de retenção, em unidades de período de retenção, para o qual salvar alterações para a *publicação*fornecida. a *retenção* é **int**, com um padrão de 14 unidades. As unidades de período de retenção são definidas por *retention_period_unit*. Se a assinatura não estiver sincronizada dentro do período de retenção e as alterações pendentes que por ventura tenha recebido tiverem sido removidas por uma operação de limpeza no Distribuidor, a assinatura irá expirar e deverá ser reiniciada. O período máximo de retenção permitido é o número de dias entre 31 de dezembro de 9999 e a data atual.  
  
> [!NOTE]  
>  O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para acomodar Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
`[ @sync_mode = ] 'sync_mode'`É o modo da sincronização inicial dos assinantes para a publicação. *sync_mode* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**nativo** (padrão)|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas.|  
|**character**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas. Necessário para dar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes e não.|  
  
`[ @allow_push = ] 'allow_push'`Especifica se as assinaturas push podem ser criadas para a publicação fornecida. *allow_push* é **nvarchar (5)**, com um padrão true, que permite assinaturas push na publicação.  
  
`[ @allow_pull = ] 'allow_pull'`Especifica se as assinaturas pull podem ser criadas para a publicação fornecida. *allow_pull* é **nvarchar (5)**, com um padrão true, que permite assinaturas pull na publicação. Você deve especificar true para os [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes de suporte.  
  
`[ @allow_anonymous = ] 'allow_anonymous'`Especifica se assinaturas anônimas podem ser criadas para a publicação fornecida. *allow_anonymous* é **nvarchar (5)**, com um padrão de true, que permite assinaturas anônimas na publicação. Para dar [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a assinantes, você deve especificar **true**.  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'`Especifica se a publicação está habilitada para a Internet e determina se o FTP (File Transfer Protocol) pode ser usado para transferir os arquivos de instantâneo para um assinante. *enabled_for_internet* é **nvarchar (5)**, com um padrão de false. Se **for true**, os arquivos de sincronização da publicação serão colocados no diretório C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp O usuário deve criar o diretório Ftp. Se for **false**, a publicação não estará habilitada para acesso à Internet.  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'`Esse parâmetro foi preterido e só tem suporte para a compatibilidade com versões anteriores de scripts. Use *conflict_logging* para especificar o local onde os registros de conflitos são armazenados.  
  
`[ @dynamic_filters = ] 'dynamic_filters'`Permite que a publicação de mesclagem Use filtros de linha com parâmetros. *dynamic_filters* é **nvarchar (5)**, com um padrão de false.  
  
> [!NOTE]  
>  Você não deve especificar esse parâmetro mas, em vez disso, permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine se filtros de linha com parâmetros estão sendo usado usados. Se você especificar um valor de **true** para *dynamic_filters*, deverá definir um filtro de linha com parâmetros para o artigo. Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'`Especifica se os arquivos de instantâneo são armazenados na pasta padrão. *snapshot_in_default_folder* é **nvarchar (5)**, com um padrão de true. Se **for true**, os arquivos de instantâneo poderão ser encontrados na pasta padrão. Se **for false**, os arquivos de instantâneo serão armazenados no local alternativo especificado pelo *alternate_snapshot_folder*. Os locais alternativos podem ser um outro servidor, uma unidade de rede ou uma mídia removível (como um CD-ROM ou discos removíveis). Você também pode salvar os arquivos de instantâneo em um site de FTP para recuperação posterior pelo Assinante. Observe que esse parâmetro pode ser verdadeiro e ainda ter um local especificado por *alt_snapshot_folder*. Essa combinação especifica que os arquivos de instantâneo serão armazenados nos locais padrão e alternativos.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`Especifica o local da pasta alternativa para o instantâneo. *alternate_snapshot_folder* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'`Especifica um ponteiro para um local de arquivo **. SQL** . *pre_snapshot_script* é **nvarchar (255)**, com um padrão de NULL. O Agente de Mesclagem executará o script pré-instantâneo antes de qualquer script de objeto replicado ao aplicar o instantâneo no Assinante. O script é executado no contexto de segurança usado pelo Agente de Mesclagem ao se conectar ao banco de dados de assinatura. Os scripts de pré-instantâneo não são [!INCLUDE[ssEW](../../includes/ssew-md.md)] executados em assinantes.  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'`Especifica um ponteiro para um local de arquivo **. SQL** . *post_snapshot_script* é **nvarchar (255)**, com um padrão de NULL. O Agente de Mesclagem executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tenham sido aplicados durante uma sincronização inicial. O script é executado no contexto de segurança usado pelo Agente de Mesclagem ao se conectar ao banco de dados de assinatura. Os scripts de pós-instantâneo não são executados em [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.  
  
`[ @compress_snapshot = ] 'compress_snapshot'`Especifica que o instantâneo gravado no local de ** \@alt_snapshot_folder** deve ser compactado no formato [!INCLUDE[msCoName](../../includes/msconame-md.md)] cab. *compress_snapshot* é **nvarchar (5)**, com um padrão de false. **false** especifica que o instantâneo não será compactado; **true** especifica que o instantâneo deve ser compactado. Arquivos de instantâneo maiores que 2 GB não podem ser compactados. Arquivos de instantâneo compactados são descompactados no local onde o Agente de Mesclagem é executado; as assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. O instantâneo na pasta padrão não pode ser compactado. Para dar [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a assinantes, você deve especificar **false**.  
  
`[ @ftp_address = ] 'ftp_address'`É o endereço de rede do serviço FTP para o distribuidor. *ftp_address* é **sysname**, com um padrão de NULL. Especifica onde os arquivos de instantâneo de publicação estão localizados para o Agente de Mesclagem de um assinante a ser coletado. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter um *ftp_address*diferente. A publicação deve oferecer suporte à propagação de instantâneos por meio de FTP.  
  
`[ @ftp_port = ] ftp_port`É o número da porta do serviço FTP para o distribuidor. *ftp_port* é **int**, com um padrão de 21. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Mesclagem ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter sua própria *ftp_port*.  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'`Especifica onde os arquivos de instantâneo estarão disponíveis para o Agente de Mesclagem do assinante a ser coletado se a publicação der suporte à propagação de instantâneos usando FTP. *ftp_subdirectory* é **nvarchar (255)**, com um padrão de NULL. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter sua própria *ftp_subdirctory* ou optar por não ter subdiretório, indicado com um valor nulo.  
  
 Na pré-geração de instantâneos para publicação com filtros com parâmetros, o instantâneo de dados de cada partição de Assinante precisa estar em sua própria pasta. A estrutura de diretório para instantâneos pré-gerados por meio de FTP deve seguir a estrutura a seguir:  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*PartitionID*.  
  
> [!NOTE]  
>  Os valores acima em itálico dependerão das especificações da publicação e da partição de Assinante.  
  
`[ @ftp_login = ] 'ftp_login'`É o nome de usuário usado para se conectar ao serviço FTP. *ftp_login* é **sysname**, com um padrão de ' Anonymous '.  
  
`[ @ftp_password = ] 'ftp_password'`É a senha de usuário usada para se conectar ao serviço FTP. *ftp_password* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
`[ @conflict_retention = ] conflict_retention`Especifica o período de retenção, em dias, para o qual os conflitos são retidos. *conflict_retention* é **int**, com um padrão de 14 dias antes que a linha de conflito seja limpa da tabela de conflitos.  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'`Especifica se as otimizações de alteração de partição devem ser habilitadas quando as partições de computação não puderem ser usadas. *keep_partition_changes* é **nvarchar (5)**, com um padrão de true. **false** significa que as alterações de partição não são otimizadas e quando as partições de computação não são usadas, as partições enviadas a todos os assinantes serão verificadas quando os dados forem alterados em uma partição. **verdadeiro** significa que as alterações de partição são otimizadas e somente os assinantes que têm linhas nas partições alteradas são afetados. Ao usar partições preputadas, defina *use_partition_groups* como **true** e defina *keep_partition_changes* como **false**. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
> [!NOTE]  
>  Se você especificar um valor de **true** para *keep_partition_changes*, especifique um valor de **1** para o parâmetro agente de instantâneo **-MaxNetworkOptimization**. Para obter mais informações sobre esse parâmetro, consulte [replicação agente de instantâneo](../../relational-databases/replication/agents/replication-snapshot-agent.md). Para obter informações sobre como especificar parâmetros de agente, consulte [Replication Agent Administration](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 Com [!INCLUDE[ssEW](../../includes/ssew-md.md)] os assinantes, *keep_partition_changes* deve ser definido como true para garantir que as exclusões sejam propagadas corretamente. Quando definido como falso, o assinante pode ter mais linhas do que o esperado.  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'`Habilita ou desabilita a capacidade de copiar os bancos de dados de assinatura que assinam essa publicação. *allow_subscription_copy* é **nvarchar (5)**, com um padrão de false. O tamanho do banco de dados de assinatura copiado deve ser menor de 2 gigabytes (GB).  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'`Lista as funções que são usadas para definir uma partição de assinante dos dados publicados quando são usados filtros de linha com parâmetros. *validate_subscriber_info* é **nvarchar (500)**, com um padrão de NULL. Essa informação é usada pelo Agente de Mesclagem para validar a partição do Assinante. Por exemplo, se [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) for usado no filtro de linha com parâmetros, o parâmetro deverá ser `@validate_subscriber_info=N'SUSER_SNAME()'`.  
  
> [!NOTE]  
>  Você não deve especificar esse parâmetro, mas sim permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automaticamente os critérios de filtragem.  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'`Esse parâmetro foi preterido e só tem suporte para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge`O número máximo de processos de mesclagem simultâneos. *maximum_concurrent_merge* é **int** com um padrão de 0. Um valor de **0** para essa propriedade significa que não há nenhum limite para o número de processos de mesclagem simultâneos em execução em um determinado momento. Essa propriedade define um limite para o número de processos de mesclagem simultâneos que pode ser executado em uma publicação de mesclagem de uma vez. Se houver mais processos de mesclagem agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de mesclagem em execução no momento seja concluído.  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots`O número máximo de sessões de Agente de Instantâneo que podem ser executadas simultaneamente para gerar instantâneos de dados filtrados para partições de assinante. *maximum_concurrent_dynamic_snapshots* é **int** com um padrão de 0. Se for **0**, não haverá nenhum limite para o número de sessões de instantâneo. Se houver mais processos de instantâneo agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de instantâneo em execução no momento seja concluído.  
  
`[ @use_partition_groups = ] 'use_partition_groups'`Especifica que as partições pré-computadas devem ser usadas para otimizar o processo de sincronização. *use_partition_groups* é **nvarchar (5)** e pode ser um destes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**true**|A publicação usa partições pré-computadas.|  
|**for**|A publicação não usa partições pré-computadas.|  
|NULL (padrão)|O sistema escolhe a estratégia de particionamento.|  
  
 Partições pré-computadas são usadas por padrão. Para evitar o uso de partições preputadas, *use_partition_groups* deve ser definido como **false**. Quando NULL, o sistema decidirá se partições pré-computadas podem ser usadas. Se as partições preputadas não puderem ser usadas, esse valor será efetivamente **falso** sem gerar erros. Nesses casos, *keep_partition_changes* pode ser definida como **true** para fornecer alguma otimização. Para obter mais informações, consulte [filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) e otimizar o [desempenho de filtro com parâmetros com partições de computação](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
`[ @publication_compatibility_level = ] backward_comp_level`Indica a compatibilidade com versões anteriores da publicação. *backward_comp_level* é **nvarchar (6)** e pode ser um destes valores:  
  
|Valor|Versão|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl`Indica se a replicação do esquema tem suporte para a publicação. *replicate_ddl* é **int**, com um padrão de 1. **1** indica que as instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas e **0** indica que as instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 O * \@parâmetro replicate_ddl* é respeitado quando uma instrução DDL adiciona uma coluna. O * \@parâmetro replicate_ddl* é ignorado quando uma instrução DDL altera ou descarta uma coluna pelos seguintes motivos.  
  
-   Quando uma coluna é removida, sysarticlecolumns deve ser atualizado para impedir que novas instruções DML incluam a coluna removida que causaria falha no agente de distribuição. O * \@parâmetro replicate_ddl* é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma coluna é alterada, o tipo de dados de origem ou nulidade podem ter sido alterados, fazendo as instruções DML conterem um valor que pode não ser compatível com a tabela no assinante. Estas instruções DML podem causar falha no agente de distribuição. O * \@parâmetro replicate_ddl* é ignorado porque a replicação sempre deve replicar a alteração de esquema.  
  
-   Quando uma instrução DDL adiciona uma nova coluna, sysarticlecolumns não inclui a nova coluna. Instruções DML não tentarão replicar dados para a nova coluna. O parâmetro é honrado porque replicar ou não replicar o DDL são aceitáveis.  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'`Indica se os assinantes dessa publicação podem iniciar o processo de instantâneo para gerar o instantâneo filtrado para sua partição de dados. *allow_subscriber_initiated_snapshot* é **nvarchar (5)**, com um padrão de false. **verdadeiro** indica que os assinantes podem iniciar o processo de instantâneo.  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'`Especifica se a publicação está habilitada para sincronização da Web. *allow_web_synchronization* é **nvarchar (5)**, com um padrão de false. **verdadeiro** especifica que as assinaturas para esta publicação podem ser sincronizadas por HTTPS. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md). Para dar [!INCLUDE[ssEW](../../includes/ssew-md.md)] suporte a assinantes, você deve especificar **true**.  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'`Especifica o valor padrão da URL da Internet usada para sincronização da Web. *web_synchronization_url i*s **nvarchar (500)**, com um padrão de NULL. Define a URL da Internet padrão se uma não for definida explicitamente quando [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) for executada.  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'`Determina se as exclusões são enviadas ao Assinante quando a modificação da linha no Publicador faz com que ela altere sua partição. *allow_partition_realignment* é **nvarchar (5)**, com um padrão de true. **verdadeiro** envia exclusões para o Assinante para refletir os resultados de uma alteração de partição removendo dados que não fazem mais parte da partição do Assinante. **false** deixa os dados de uma partição antiga no Assinante, em que as alterações feitas a esses dados no Publicador não serão replicadas para esse assinante, mas as alterações feitas no Assinante serão replicadas para o Publicador. Definir *allow_partition_realignment* como **false** é usado para reter dados em uma assinatura de uma partição antiga quando os dados precisam ser acessíveis para fins históricos.  
  
> [!NOTE]  
>  Os dados que permanecem no Assinante como resultado da definição de *allow_partition_realignment* como **false** devem ser tratados como se fossem somente leitura; no entanto, isso não é imposto pelo sistema de replicação.  
  
`[ @retention_period_unit = ] 'retention_period_unit'`Especifica as unidades para o período de retenção definido por *retenção*. *retention_period_unit* é **nvarchar (10)** e pode ser um dos valores a seguir.  
  
|Valor|Versão|  
|-----------|-------------|  
|**dia** (padrão)|O período de retenção é especificado em dias.|  
|**week**|O período de retenção é especificado em semanas.|  
|**month**|O período de retenção é especificado em meses.|  
|**year**|O período de retenção é especificado em anos.|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold`Especifica o número de alterações que estão contidas em uma geração. Uma geração é uma coleção de alterações que é entregue a um Publicador ou Assinante. *generation_leveling_threshold* é **int**, com um valor padrão de 1000.  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy`Especifica se as alterações são carregadas do assinante antes de uma reinicialização automática exigida por uma alteração na publicação, em que um valor de **1** foi especificado para ** \@force_reinit_subscription**. *automatic_reinitialization_policy* é bit, com um valor padrão de 0. **1** significa que as alterações são carregadas do assinante antes que ocorra uma reinicialização automática.  
  
> [!IMPORTANT]  
>  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
`[ @conflict_logging = ] 'conflict_logging'`Especifica onde os registros de conflitos são armazenados. *conflict_logging* é **nvarchar (15)** e pode ser um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Publicador**|Registros de conflito são armazenados no Publicador.|  
|**Assinante**|Registros de conflito são armazenados no Assinante que causou o conflito. Sem suporte para [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.|  
|**ambos**|Registros de conflito são armazenados no Publicador e no Assinante.|  
|NULL (padrão)|A replicação define automaticamente *conflict_logging* para ambos quando o valor *backward_comp_level* é **90RTM** e para **o** **Publicador** em todos os outros casos.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepublication** é usado na replicação de mesclagem.  
  
 Para listar objetos de publicação para o Active Directory ** \@** usando o parâmetro add_to_active_directory [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o objeto já deve ser criado no Active Directory.  
  
 Se existirem várias publicações que publiquem o mesmo objeto de banco de dados, somente as publicações com um *replicate_ddl* valor de **1** REPLICARÃO as instruções ALTER TABLE, ALTER View, ALTER PROCEDURE, ALTER FUNCTION e ALTER TRIGGER DDL. No entanto, uma instrução ALTER TABLE DROP COLUMN DDL será replicada por todas as publicações que estão publicando a coluna cancelada.  
  
 Para [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, o valor de *alternate_snapshot_folder* é usado somente quando o valor de *snapshot_in_default_folder* é **false**.  
  
 Com a replicação DDL habilitada (_replicate_ddl_**= 1**) para uma publicação, a fim de fazer alterações de DDL não replicadas na publicação, [sp_changemergepublication &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) deve ser executada primeiro para definir *replicate_ddl* como **0**. Depois que as instruções DDL de não replicação forem emitidas, **sp_changemergepublication** poderá ser executado novamente para ativar novamente a replicação DDL.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergepublication**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepublication](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
