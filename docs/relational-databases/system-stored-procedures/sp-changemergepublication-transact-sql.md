---
title: sp_changemergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepublication_TSQL
- sp_changemergepublication
helpviewer_keywords:
- sp_changemergepublication
ms.assetid: 81fe1994-7678-4852-980b-e02fedf1e796
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bcedfb666b5fffb2f31b6bf73ee02972ea30067
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097679"
---
# <a name="sp_changemergepublication-transact-sql"></a>sp_changemergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de uma publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergepublication [ @publication= ] 'publication'  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`O nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`A propriedade a ser alterada para a publicação fornecida. a *Propriedade* é **sysname**e pode ser um dos valores listados na tabela a seguir.  
  
`[ @value = ] 'value'`O novo valor para a propriedade especificada. *Value* é **nvarchar (255)** e pode ser um dos valores listados na tabela a seguir.  
  
 Essa tabela descreve as propriedades da publicação que podem ser alteradas e as restrições nos valores dessas propriedades.  
  
|Propriedade|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Assinaturas anônimas são permitidas.|  
||**for**|Assinaturas anônimas não são permitidas.|  
|**allow_partition_realignment**|**true**|Exclusões são enviadas para o Assinante para refletir os resultados de uma alteração de partição, removendo dados que não pertencem mais à partição do Assinante. Esse é o comportamento padrão.|  
||**for**|Dados de uma partição antiga serão deixados no Assinante, onde as alterações feitas nesses dados no Publicador não serão replicadas para esse Assinante. Em vez disso, as alterações feitas no Assinante serão replicadas no Publicador. Isso é usado para reter dados em uma assinatura de uma partição antiga quando os dados precisam estar acessíveis para fins de histórico.|  
|**allow_pull**|**true**|São permitidas assinaturas pull para a publicação determinada.|  
||**for**|Não são permitidas assinaturas pull para a publicação determinada.|  
|**allow_push**|**true**|São permitidas assinaturas push para a publicação determinada.|  
||**for**|Não são permitidas assinaturas push para a publicação determinada.|  
|**allow_subscriber_initiated_snapshot**|**true**|O Assinante pode iniciar o processo de instantâneo.|  
||**for**|O Assinante não pode iniciar o processo de instantâneo.|  
|**allow_subscription_copy**|**true**|Você pode copiar os bancos de dados de assinatura que assinam essa publicação.|  
||**for**|Você não pode copiar os bancos de dados de assinatura que assinam essa publicação.|  
|**allow_synctoalternate**|**true**|Permite um parceiro padrão de sincronização alternativo para fazer a sincronização com esse Publicador.|  
||**for**|Não permite um parceiro padrão de sincronização alternativo para fazer a sincronização com esse Publicador.|  
|**allow_web_synchronization**|**true**|As assinaturas podem ser sincronizadas pelo HTTP.|  
||**for**|As assinatura não podem ser sincronizadas pelo HTTP.|  
|**alt_snapshot_folder**||Especifica o local da pasta alternativa para o instantâneo.|  
|**automatic_reinitialization_policy**|**1**|As alterações são carregadas do Assinante antes que a assinatura seja reiniciada.|  
||**0**|A assinatura é reiniciada sem primeiro carregar as alterações.|  
|**centralized_conflicts**|**true**|Todos os registros de conflito são armazenados no Publicador. Se você alterar esta propriedade, os Assinantes existentes deverão ser reinicializados.|  
||**for**|Os registros de conflito são armazenados no servidor que perdeu na resolução de conflito. Se você alterar esta propriedade, os Assinantes existentes deverão ser reinicializados.|  
|**compress_snapshot**|**true**|O instantâneo em uma pasta de instantâneo alternativa é compactado no formato CAB. O instantâneo na pasta de instantâneo padrão não pode ser compactado. A alteração dessa propriedade requer um novo instantâneo.|  
||**for**|Por padrão, o instantâneo não é compactado. A alteração dessa propriedade requer um novo instantâneo.|  
|**conflict_logging**|**Publicador**|Registros de conflito são armazenados no Publicador.|  
||**Assinante**|Registros de conflito são armazenados no Assinante que causou o conflito. Sem suporte para [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes *.*|  
||**ambos**|Registros de conflito são armazenados no Publicador e no Assinante.|  
|**conflict_retention**||Um **int** que especifica o período de retenção, em dias, para o qual os conflitos são retidos. Definir *conflict_retention* como **0** significa que nenhuma limpeza de conflito é necessária.|  
|**ndescrição**||Descrição da publicação.|  
|**dynamic_filters**|**true**|Publicação é filtrada com base em uma cláusula dinâmica.|  
||**for**|A publicação não é filtrada dinamicamente.|  
|**enabled_for_internet**|**true**|A publicação está habilitada para a Internet. O FTP (Protocolo de Transferência de Arquivo) pode ser usado para transferir os arquivos de instantâneo para um Assinante. Os arquivos de sincronização para a publicação são colocados no diretório C:\Arquivos de Programas\Microsoft SQL Server\MSSQL\Repldata\ftp.|  
||**for**|A publicação não está habilitada para a Internet.|  
|**ftp_address**||O endereço de rede do serviço FTP para o Distribuidor. Especifica onde são armazenados arquivos de instantâneo de publicação.|  
|**ftp_login**||O nome de usuário usado na conexão com o serviço de FTP.|  
|**ftp_password**||A senha de usuário usada na conexão com o serviço de FTP.|  
|**ftp_port**||O número da porta do serviço FTP do Distribuidor. Especifica o número da porta TCP do site de FTP onde os arquivos de instantâneo de publicação são armazenados.|  
|**ftp_subdirectory**||Especifica onde os arquivos de instantâneo são criados se a publicação oferecer suporte a instantâneos de propagação usando o FTP.|  
|**generation_leveling_threshold**|**int**|Especifica o número de alterações que estão contidas em uma geração. Uma geração é uma coleção de alterações que é entregue a um Publicador ou Assinante.|  
|**keep_partition_changes**|**true**|A sincronização é otimizada e somente Assinantes com linhas nas partições alteradas são afetados. A alteração dessa propriedade requer um novo instantâneo.|  
||**for**|A sincronização não será otimizada e as partições que são enviadas a todos os Assinantes serão verificadas quando os dados forem alterados em uma partição. A alteração dessa propriedade requer um novo instantâneo.|  
|**max_concurrent_merge**||Esse é um **int** que representa o número máximo de processos de mesclagem simultâneos que podem ser executados em uma publicação. Se for 0, não há limite. Se um número maior de processos de mesclagem for agendado para execução ao mesmo tempo, os trabalhos em excesso serão enfileirados e esperarão até que um processo de mesclagem atual seja concluído.|  
|**max_concurrent_dynamic_snapshots**||Esse é um **int** que representa o número máximo de sessões de instantâneo para gerar um instantâneo de dados filtrado que pode ser executado simultaneamente em uma publicação de mesclagem que usa filtros de linha com parâmetros. Se for **0**, não haverá limite. Se um número maior de processos de instantâneo for agendado para execução ao mesmo tempo, os trabalhos em excesso serão enfileirados e esperarão até que o processo de mesclagem atual seja concluído.|  
|**post_snapshot_script**||Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Distribuição ou Agente de Mesclagem executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tentam sido aplicados durante uma sincronização inicial. A alteração dessa propriedade requer um novo instantâneo.|  
|**pre_snapshot_script**||Especifica um ponteiro para um local de arquivo **. SQL** . O Agente de Mesclagem executará o script pré-instantâneo antes de qualquer script de objeto replicado, ao aplicar um instantâneo no Assinante. A alteração dessa propriedade requer um novo instantâneo.|  
|**publication_compatibility_level**|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
||**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**publish_to_activedirectory**|**true**|Esse parâmetro foi preterido e tem suporte somente para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação no Active Directory.|  
||**for**|Remove as informações de publicação do Active Directory.|  
|**replicate_ddl**|**1**|Instruções DDL (Linguagem de Definição de Dados) executadas no Publicador são replicadas.|  
||**0**|Instruções DDL não são replicadas.|  
|**políticas**||Esse é um **int** que representa o número de unidades de *retention_period_unit* para as quais salvar as alterações para a publicação fornecida. Se a assinatura não estiver sincronizada dentro do período de retenção e as alterações pendentes que por ventura tenha recebido tiverem sido removidas por uma operação de limpeza no Distribuidor, a assinatura irá expirar e deverá ser reiniciada. O período máximo de retenção permitido é o número de dias entre 31 de dezembro de 9999 e a data atual.<br /><br /> Observação: o período de retenção para publicações de mesclagem tem um período de carência de 24 horas para acomodar assinantes em fusos horários diferentes.|  
|**retention_period_unit**|**day**|O período de retenção é especificado em dias.|  
||**week**|O período de retenção é especificado em semanas.|  
||**month**|O período de retenção é especificado em meses.|  
||**year**|O período de retenção é especificado em anos.|  
|**snapshot_in_defaultfolder**|**true**|Arquivos de instantâneo são armazenados na pasta de instantâneos padrão.|  
||**for**|Os arquivos de instantâneo são armazenados no local alternativo especificado por *alt_snapshot_folder*. Essa combinação especifica que os arquivos de instantâneo são armazenados nos locais padrão e alternativo.|  
|**snapshot_ready**|**true**|Instantâneo disponível para a publicação.|  
||**for**|Instantâneo não disponível para a publicação.|  
|**Estado**|**ativo**|Publicação com status ativo.|  
||**inativo**|Publicação com status inativo.|  
|**sync_mode**|**nativo** ou<br /><br /> **bcp nativo**|Saída de programa de cópia em massa em modo nativo de todas as tabelas é usada para o instantâneo inicial.|  
||**character**<br /><br /> ou **caractere bcp**|Saída de programa de cópia em massa em modo de caractere de todas as tabelas é usada para o instantâneo inicial, que é exigido de todos os Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**use_partition_groups**<br /><br /> Observação: depois de usar partition_groups, se você voltar a usar **SetupBelongs**e definir **use_partition_groups = false** em **changemergearticle**, isso poderá não ser refletido corretamente depois que um instantâneo for obtido. Os gatilhos que são gerados através do instantâneo são compatíveis com grupos de partição.<br /><br /> A solução alternativa para esse cenário é definir o status como inativo, modificar o **use_partition_groups**e, em seguida, definir status como ativo.|**true**|A publicação usa partições pré-computadas.|  
||**for**|A publicação não usa partições pré-computadas.|  
|**validate_subscriber_info**||Lista as funções que estão sendo usadas para recuperar informações do Assinante. Depois, valida o critério de filtro dinâmico que está sendo usado pelo Assinante para verificar se as informações serão particionadas consistentemente.|  
|**web_synchronization_url**||Valor padrão do URL da Internet usado para sincronização da Web.|  
|NULL (padrão)||Retorna a lista de valores com suporte para a *Propriedade*.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que a alteração da publicação não invalidará o instantâneo. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que a alteração da publicação pode invvalidate o instantâneo. Se houver assinaturas existentes que exijam um novo instantâneo, o dará permissão para que o instantâneo existente seja marcado como obsoleto e que um novo instantâneo seja gerado.  
  
 Consulte a seção Comentários para obter as propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** especifica que a alteração da publicação não exige que as assinaturas sejam reinicializadas. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que a alteração da publicação faz com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
 Consulte a seção Comentários para as propriedades que, quando alteradas, requerem que todas as assinaturas existentes sejam reiniciadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergepublication** é usado na replicação de mesclagem.  
  
 Alterar as propriedades a seguir requer que um instantâneo novo seja gerado. Você deve especificar um valor de **1** para o parâmetro *force_invalidate_snapshot* .  
  
-   **alt_snapshot_folder**  
  
-   **compress_snapshot**  
  
-   **dynamic_filters**  
  
-   **ftp_address**  
  
-   **ftp_login**  
  
-   **ftp_password**  
  
-   **ftp_port**  
  
-   **ftp_subdirectory**  
  
-   **post_snapshot_script**  
  
-   **publication_compatibility_level** (somente para **80SP3** )  
  
-   **pre_snapshot_script**  
  
-   **snapshot_in_defaultfolder**  
  
-   **sync_mode**  
  
-   **use_partition_groups**  
  
 Alterar as propriedades a seguir requer que assinaturas existentes sejam reinicializadas. Você deve especificar um valor de **1** para o parâmetro *force_reinit_subscription* .  
  
-   **dynamic_filters**  
  
-   **validate_subscriber_info**  
  
 Para listar objetos de publicação para Active Directory usando o *publish_to_active_directory*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o objeto já deve ter sido criado no Active Directory.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changemergepublication](../../relational-databases/replication/codesnippet/tsql/sp-changemergepublicatio_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changemergepublication**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepublication](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
