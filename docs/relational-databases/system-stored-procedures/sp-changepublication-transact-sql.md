---
title: sp_changepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45c61b33a7cc1669ae34f7888fda1450524b079b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536811"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, com um padrão NULL.  
  
`[ @property = ] 'property'` É a propriedade de publicação a alterar. *propriedade* está **nvarchar (255)**.  
  
`[ @value = ] 'value'` É o novo valor da propriedade. *valor* está **nvarchar (255)**, com um padrão NULL.  
  
 Essa tabela descreve as propriedades da publicação que podem ser alteradas e restrições nos valores dessas propriedades.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Podem ser criadas assinaturas anônimas para a publicação determinada, e *immediate_sync* também deverá ser **verdadeiro**. Não pode ser alterado para publicações ponto a ponto.|  
||**false**|Não podem ser criadas assinaturas anônimas para a publicação determinada. Não pode ser alterado para publicações ponto a ponto.|  
|**allow_initialize_from_backup**|**true**|Os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. Essa propriedade não pode ser alterada para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações.|  
||**false**|Assinantes devem usar o instantâneo inicial. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_partition_switch**|**true**|ALTER TABLE... Instruções SWITCH podem ser executadas no banco de dados publicado. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ALTER TABLE... Instruções SWITCH não podem ser executadas no banco de dados publicado.|  
|**allow_pull**|**true**|São permitidas assinaturas pull para a publicação determinada. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|Não são permitidas assinaturas pull para a publicação determinada. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_push**|**true**|São permitidas assinaturas push para a publicação determinada.|  
||**false**|Não são permitidas assinaturas push para a publicação determinada.|  
|**allow_subscription_copy**|**true**|Habilita a capacidade de copiar bancos de dados que assinam esta publicação. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|Desabilita a capacidade de copiar bancos de dados que assinam esta publicação. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**alt_snapshot_folder**||Local da pasta alternativa para o instantâneo.|  
|**centralized_conflicts**|**true**|Registros de conflito são armazenados no Publicador. Só poderá ser alterado se não houver nenhuma assinatura ativa. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|Registros de conflito são armazenados no Publicador e no Assinante que causou o conflito. Só poderá ser alterado se não houver nenhuma assinatura ativa. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**compress_snapshot**|**true**|Instantâneo em uma pasta de instantâneo alternativa é compactado no formato de arquivo .cab. O instantâneo na pasta de instantâneo padrão não pode ser compactado.|  
||**false**|O instantâneo não é compactado, o que é o comportamento padrão para replicação.|  
|**conflict_policy**|**wins pub**|Política de resolução de conflito para atualizar Assinantes em que o Publicador vence o conflito. Essa propriedade só poderá ser alterada se não houver assinaturas ativas. Sem suporte para Publicadores Oracle.|  
||**sub reinit**|Na atualização de Assinantes, se ocorrer um conflito a assinatura deverá ser reiniciada. Essa propriedade só poderá ser alterada se não houver assinaturas ativas. Sem suporte para Publicadores Oracle.|  
||**sub wins**|Política de resolução de conflito para atualização de Assinantes onde o Assinante vence o conflito. Essa propriedade só poderá ser alterada se não houver assinaturas ativas. Sem suporte para Publicadores Oracle.|  
|**conflict_retention**||**int** que especifica o período de retenção de conflito, em dias. A retenção padrão é 14 dias. **0** significa que nenhuma limpeza de conflito é necessária. Sem suporte para Publicadores Oracle.|  
|**description**||Entrada opcional que descreve a publicação.|  
|**enabled_for_het_sub**|**true**|Permite que a publicação dê suporte a Assinantes que não são do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **enabled_for_het_sub** não pode ser alterado quando existem assinaturas na publicação. Talvez você precise executar [procedimentos armazenados de replicação (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) estar em conformidade com os seguintes requisitos antes de definir **enabled_for_het_sub** como true:<br /> - **allow_queued_tran** deve ser **falso**.<br /> - **allow_sync_tran** deve ser **falso**.<br /> Alterando **enabled_for_het_sub** à **verdadeiro** podem alterar configurações de publicação existentes. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|A publicação não dá suporte a Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_internet**|**true**|A publicação é habilitada para a Internet, e o FTP (File Transfer Protocol) pode ser usado para transferir os arquivos de instantâneo a um assinante. Os arquivos de sincronização para a publicação são colocados no seguinte diretório: C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp. *ftp_address* não pode ser NULL. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|A publicação não está habilitada para a Internet. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_p2p**|**true**|A publicação oferece suporte a replicação ponto a ponto. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /> Para definir **enabled_for_p2p** à **verdadeiro**, as seguintes restrições se aplicam:<br /> - **allow_anonymous** deve ser **false**<br /> - **allow_dts** deve ser **falso**.<br /> - **allow_initialize_from_backup** deve ser **true**<br /> - **allow_queued_tran** deve ser **falso**.<br /> - **allow_sync_tran** deve ser **falso**.<br /> - **enabled_for_het_sub** deve ser **falso**.<br /> - **independent_agent** deve ser **verdadeiro**.<br /> - **repl_freq** deve ser **contínua**.<br /> - **replicate_ddl** deve ser **1**.|  
||**false**|A publicação não oferece suporte a replicação ponto a ponto. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_address**||Local acessível de FTP dos arquivos de instantâneo de publicação. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_login**||Nome de usuário para conexão com o serviço de FTP e o valor ANONYMOUS são permitidos. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_password**||Senha para o nome de usuário usado na conexão com o serviço de FTP. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_port**||Número da porta do serviço FTP para Distribuidor. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_subdirectory**||Especifica onde os arquivos de instantâneo são criados se a publicação oferece suporte à propagação de instantâneo usando FTP. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**immediate_sync**|**true**|Arquivos de sincronização para a publicação são criados ou recriados em cada execução do Snapshot Agent. Assinantes podem receber arquivos de sincronização imediatamente após a assinatura, se o Snapshot Agent foi concluído uma vez antes da assinatura. Novas assinaturas obtêm os arquivos de sincronização mais novos gerados pela execução mais recente do Agente de Instantâneo. *independent_agent* também deve ser **verdadeiro**. Consulte os comentários abaixo para obter mais informações **immediate_sync**.|  
||**false**|Arquivos de sincronização só serão criados se houver novas assinaturas. Assinantes não podem receber arquivos de sincronização após a assinatura até que o Snapshot Agent seja iniciado e concluído.|  
|**independent_agent**|**true**|A publicação tem seu próprio Distribution Agent dedicado.|  
||**false**|A publicação usa um Distribution Agent compartilhado e cada par de banco de dados de publicação/assinatura tem um agente compartilhado.|  
|**p2p_continue_onconflict**|**true**|O Distribution Agent continua processando alterações quando um conflito é detectado.<br /> **Cuidado:** É recomendável que você use o valor padrão de `FALSE`. Quando essa opção é definida como `TRUE`, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem a maior ID de originador. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
||**false**|O Distribution Agent deixa de processar alterações quando um conflito é detectado.|  
|**post_snapshot_script**||Especifica o local de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que o Distribution Agent executa depois que todos os outros scripts de objetos e dados replicados foram aplicados durante uma sincronização inicial.|  
|**pre_snapshot_script**||Especifica o local de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que o Distribution Agent executa antes que todos os outros scripts de objetos e dados replicados sejam aplicados durante uma sincronização inicial.|  
|**publish_to_ActiveDirectory**|**true**|Esse parâmetro foi preterido e tem suporte somente para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.|  
||**false**|Remove as informações de publicação do Active Directory.|  
|**queue_type**|**sql**|Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações. Essa propriedade só poderá ser alterada se não houver assinaturas ativas.<br /><br /> Observação: O suporte para uso do Serviço de Enfileiramento de Mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)] foi descontinuado. Especificando um valor de **msmq** para *valor* resulta em um erro.|  
|**repl_freq**|**contínua**|Publica saída de todas as transações com base em log.|  
||**snapshot**|Publica somente eventos de sincronização agendados.|  
|**replicate_ddl**|**1**|Instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0**|Instruções DDL não são replicadas. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A replicação de alterações de esquema não pode ser desabilitada ao usar replicação ponto a ponto.|  
|**replicate_partition_switch**|**true**|ALTER TABLE... Instruções SWITCH que são executadas no banco de dados publicado devem ser replicadas para assinantes. Essa opção é válida somente se *allow_partition_switch* é definida como TRUE. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ALTER TABLE... Instruções SWITCH não devem ser replicadas para assinantes.|  
|**retention**||**int** que representa o período de retenção, em horas, para a atividade de assinatura. Se uma assinatura não estiver ativa dentro do período de retenção, será removida.|  
|**snapshot_in_defaultfolder**|**true**|Arquivos de instantâneo são armazenados na pasta de instantâneos padrão. Se *alt_snapshot_folder*também for especificado, os arquivos de instantâneo são armazenados em ambos os locais padrão e alternativo.|  
||**false**|Arquivos de instantâneo são armazenados no local alternativo especificado por *alt_snapshot_folder*.|  
|**status**|**active**|Dados de Publicação estão imediatamente disponíveis para os Assinantes quando a publicação é criada. Sem suporte para Publicadores Oracle.|  
||**inactive**|Dados de Publicação não estão disponíveis para os Assinantes quando a publicação é criada. Sem suporte para Publicadores Oracle.|  
|**sync_method**|**native**|Usa saída de cópia em massa do modo nativo de todas as tabelas ao sincronizar assinaturas.|  
||**character**|Usa saída de cópia em massa do modo de caractere de todas as tabelas ao sincronizar assinaturas.|  
||**concurrent**|Usa saída de programa de cópia em massa do modo nativo de todas as tabelas, mas não bloqueia as tabelas durante o processo de geração de instantâneo. Não válido para replicação de instantâneo.|  
||**concurrent_c**|Usa saída de programa de cópia em massa do modo de caractere de todas as tabelas, mas não bloqueia as tabelas durante o processo de geração de instantâneo. Não válido para replicação de instantâneo.|  
|**taskid**||Essa propriedade foi preterida e não tem mais suporte.|  
|**allow_drop**|**true**|Habilita `DROP TABLE` DLL de suporte para artigos que fazem parte da replicação transacional. Versão mínima com suporte: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 ou superior e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1 ou superior. Referência adicional: [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|Desabilita `DROP TABLE` DLL de suporte para artigos que fazem parte da replicação transacional. Esse é o **padrão** valor para essa propriedade.|
|**NULL** (default)||Retorna a lista de valores com suporte para *propriedade*.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  - **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  - **1** Especifica que as alterações no artigo podem invalidar o instantâneo ser inválido. Se houver assinaturas existentes que exigem um novo instantâneo, esse valor dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.   
Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
[**@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  - **0** Especifica que as alterações no artigo fazem com que a assinatura seja reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  - **1** Especifica que as alterações no artigo fazem com que a assinatura existente seja reiniciada e dá permissão para que ocorra a reinicialização da assinatura.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
  > [!NOTE]  
  >  *Publisher* não deve ser usado ao alterar as propriedades do artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changepublication** é usado em replicação de instantâneo e replicação transacional.  
  
 Depois de alterar qualquer uma das propriedades a seguir, você deve gerar um novo instantâneo, e você deve especificar um valor de **1** para o *force_invalidate_snapshot* parâmetro.  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
Para listar objetos de publicação no Active Directory usando o **publish_to_active_directory** parâmetro, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto já deve ser criado no Active Directory.  
  
## <a name="impact-of-immediate-sync"></a>Impacto da sincronização imediata  
 Quando a sincronização imediata estiver ativada, todas as alterações no log são controladas imediatamente depois que o instantâneo inicial for gerado, mesmo se não houver nenhuma assinatura. As alterações registradas são usadas quando um cliente estiver usando o backup para adicionar um novo nó par. Depois que o backup for restaurado, o par está sincronizado com quaisquer outras alterações que ocorrem após o backup foi feito. Uma vez que os comandos são rastreados no banco de dados de distribuição, a lógica de sincronização pode examinar o último backup LSN e usá-lo como um ponto de partida, sabendo que o comando está disponível se o backup foi feito dentro do período de retenção máximo. (O valor padrão para o período de retenção mínimo é o período de retenção 0 horas e o máximo é 24 horas.)  
  
 Quando a sincronização imediata for desativada, as alterações são mantidas pelo menos durante o período de retenção mínimo e limpas imediatamente para todas as transações já replicadas. Se a sincronização imediata for desativada e estiver configurada com o período de retenção padrão, provavelmente as alterações necessárias após a realização do backup foram limpas, e novo nó par não será inicializado corretamente. A única opção restante é a confirmação da topologia. A ativação da sincronização imediata oferece maior flexibilidade e é a configuração recomendada para a replicação P2P.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_changepublication**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
