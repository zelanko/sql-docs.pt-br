---
title: sp_changepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e86b9a77a7b84a54b0e452a2e93dae9167492167
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993844"
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
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão NULL.  
  
 [  **@property =** ] **'***propriedade***'**  
 É a propriedade da publicação a ser alterada. *propriedade* é **nvarchar (255)**.  
  
 [  **@value =** ] **'***valor***'**  
 É o novo valor da propriedade. *valor* é **nvarchar (255)**, com um padrão NULL.  
  
 Essa tabela descreve as propriedades da publicação que podem ser alteradas e restrições nos valores dessas propriedades.  
  
|Propriedade|Value|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Podem ser criadas assinaturas anônimas para a publicação determinada, e *immediate_sync* também deve ser **true**. Não pode ser alterado para publicações ponto a ponto.|  
||**false**|Não podem ser criadas assinaturas anônimas para a publicação determinada. Não pode ser alterado para publicações ponto a ponto.|  
|**allow_initialize_from_backup**|**true**|Os Assinantes podem iniciar uma assinatura para essa publicação de um backup em vez de um instantâneo inicial. Essa propriedade não pode ser alterada para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações.|  
||**false**|Assinantes devem usar o instantâneo inicial. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_partition_switch**|**true**|As instruções ALTER TABLE…SWITCH podem ser executadas no banco de dados publicado. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|As instruções ALTER TABLE…SWITCH não podem ser executadas no banco de dados publicado.|  
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
|**Descrição**||Entrada opcional que descreve a publicação.|  
|**enabled_for_het_sub**|**true**|Permite que a publicação dê suporte a Assinantes que não são do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **enabled_for_het_sub** não pode ser alterado quando há assinaturas na publicação. Talvez você precise executar [procedimentos armazenados de replicação (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) de acordo com os seguintes requisitos antes de definir **enabled_for_het_sub** como true:<br /> - **allow_queued_tran** devem ser **false**.<br /> - **allow_sync_tran** devem ser **false**.<br /> Alterar **enabled_for_het_sub** para **true** pode alterar as configurações de publicação existente. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|A publicação não dá suporte a Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_internet**|**true**|A publicação é habilitada para a Internet, e o FTP (File Transfer Protocol) pode ser usado para transferir os arquivos de instantâneo a um assinante. Os arquivos de sincronização da publicação são colocados no seguinte diretório: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL\Repldata\ftp. *ftp_address* não pode ser NULL. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|A publicação não está habilitada para a Internet. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_p2p**|**true**|A publicação oferece suporte a replicação ponto a ponto. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /> Para definir **enabled_for_p2p** para **true**, as seguintes restrições se aplicam:<br /> - **allow_anonymous** devem ser **false**<br /> - **allow_dts** devem ser **false**.<br /> - **allow_initialize_from_backup** devem ser **true**<br /> - **allow_queued_tran** devem ser **false**.<br /> - **allow_sync_tran** devem ser **false**.<br /> - **enabled_for_het_sub** devem ser **false**.<br /> - **independent_agent** devem ser **true**.<br /> - **repl_freq** devem ser **contínua**.<br /> - **replicate_ddl** devem ser **1**.|  
||**false**|A publicação não oferece suporte a replicação ponto a ponto. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_address**||Local acessível de FTP dos arquivos de instantâneo de publicação. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_login**||Nome de usuário para conexão com o serviço de FTP e o valor ANONYMOUS são permitidos. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_password**||Senha para o nome de usuário usado na conexão com o serviço de FTP. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_port**||Número da porta do serviço FTP para Distribuidor. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_subdirectory**||Especifica onde os arquivos de instantâneo são criados se a publicação oferece suporte à propagação de instantâneo usando FTP. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**immediate_sync**|**true**|Arquivos de sincronização para a publicação são criados ou recriados em cada execução do Snapshot Agent. Assinantes podem receber arquivos de sincronização imediatamente após a assinatura, se o Snapshot Agent foi concluído uma vez antes da assinatura. Novas assinaturas obtêm os arquivos de sincronização mais novos gerados pela execução mais recente do Agente de Instantâneo. *independent_agent* também deve ser **true**. Consulte os comentários abaixo para obter informações adicionais **immediate_sync**.|  
||**false**|Arquivos de sincronização só serão criados se houver novas assinaturas. Assinantes não podem receber arquivos de sincronização após a assinatura até que o Snapshot Agent seja iniciado e concluído.|  
|**independent_agent**|**true**|A publicação tem seu próprio Distribution Agent dedicado.|  
||**false**|A publicação usa um Distribution Agent compartilhado e cada par de banco de dados de publicação/assinatura tem um agente compartilhado.|  
|**p2p_continue_onconflict**|**true**|O Distribution Agent continua processando alterações quando um conflito é detectado.<br /> **Cuidado:** é recomendável que você use o valor padrão de `FALSE`. Quando essa opção é definida como `TRUE`, o Distribution Agent tenta convergir os dados na topologia aplicando a linha conflitante do nó que tem o maior ID de originador. Esse método não garante convergência. Verifique se a topologia está consistente depois que um conflito é detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
||**false**|O Distribution Agent deixa de processar alterações quando um conflito é detectado.|  
|**post_snapshot_script**||Especifica o local de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que o Distribution Agent executa depois que todos os outros scripts de objetos e dados replicados foram aplicados durante uma sincronização inicial.|  
|**pre_snapshot_script**||Especifica o local de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que o Distribution Agent executa antes que todos os outros scripts de objetos e dados replicados sejam aplicados durante uma sincronização inicial.|  
|**publish_to_ActiveDirectory**|**true**|Esse parâmetro foi preterido e tem suporte somente para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.|  
||**false**|Remove as informações de publicação do Active Directory.|  
|**queue_type**|**sql**|Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenar transações. Essa propriedade só poderá ser alterada se não houver assinaturas ativas.<br /><br /> Observação: O suporte para o uso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens foi descontinuado. Especificando um valor de **msmq** para *valor* resulta em um erro.|  
|**repl_freq**|**Contínua**|Publica saída de todas as transações com base em log.|  
||**Instantâneo**|Publica somente eventos de sincronização agendados.|  
|**replicate_ddl**|**1**|Instruções DDL (linguagem de definição de dados) executadas no Publicador são replicadas. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0**|Instruções DDL não são replicadas. Essa propriedade não pode ser alterada em publicações que não sejam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A replicação de alterações de esquema não pode ser desabilitada ao usar replicação ponto a ponto.|  
|**replicate_partition_switch**|**true**|As instruções ALTER TABLE…SWITCH que são executadas no banco de dados publicado devem ser replicadas para Assinantes. Essa opção é válida somente se *allow_partition_switch* está definida como TRUE. Para obter mais informações, consulte [Replicar tabelas e índices particionados](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|As instruções ALTER TABLE…SWITCH que não devem ser replicadas para Assinantes.|  
|**retention**||**int** que representa o período de retenção, em horas, para a atividade de assinatura. Se uma assinatura não estiver ativa dentro do período de retenção, será removida.|  
|**snapshot_in_defaultfolder**|**true**|Arquivos de instantâneo são armazenados na pasta de instantâneos padrão. Se *alt_snapshot_folder*também for especificado, os arquivos de instantâneo são armazenados em ambos os locais padrão e alternativos.|  
||**false**|Arquivos de instantâneo são armazenados no local alternativo especificado por *alt_snapshot_folder*.|  
|**status**|**Ativo**|Dados de Publicação estão imediatamente disponíveis para os Assinantes quando a publicação é criada. Sem suporte para Publicadores Oracle.|  
||**Inativo**|Dados de Publicação não estão disponíveis para os Assinantes quando a publicação é criada. Sem suporte para Publicadores Oracle.|  
|**sync_method**|**native**|Usa saída de cópia em massa do modo nativo de todas as tabelas ao sincronizar assinaturas.|  
||**character**|Usa saída de cópia em massa do modo de caractere de todas as tabelas ao sincronizar assinaturas.|  
||**simultâneas**|Usa saída de programa de cópia em massa do modo nativo de todas as tabelas, mas não bloqueia as tabelas durante o processo de geração de instantâneo. Não válido para replicação de instantâneo.|  
||**concurrent_c**|Usa saída de programa de cópia em massa do modo de caractere de todas as tabelas, mas não bloqueia as tabelas durante o processo de geração de instantâneo. Não válido para replicação de instantâneo.|  
|**TaskID**||Essa propriedade foi preterida e não tem mais suporte.|  
|**allow_drop**|**true**|Permite `DROP TABLE` DLL suporte para artigos que fazem parte da replicação transacional. Versão mínima com suporte: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 ou posterior e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1 ou posterior. Referência adicional: [3170123 KB](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|Desabilita `DROP TABLE` DLL suporte para artigos que fazem parte da replicação transacional. Este é o **padrão** valor para essa propriedade.|
|**NULO** (padrão)||Retorna a lista de valores com suporte para *propriedade*.|  
  
[  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  - **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  - **1** Especifica que as alterações no artigo podem invalidar o instantâneo seja inválido. Se houver assinaturas existentes que exigem um novo instantâneo, esse valor dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.   
Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
[ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  - **0** Especifica que as alterações no artigo fazem com que a assinatura ser reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  - **1** Especifica que as alterações no artigo fazem com que a assinatura existente seja reiniciada e dá permissão para que ocorra a reinicialização da assinatura.  
  
[ **@publisher** =] **'***publicador***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
  > [!NOTE]  
  >  *publicador* não deve ser usado ao alterar as propriedades de artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
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
 Quando a sincronização imediata estiver ativada, todas as alterações no log são controladas imediatamente depois que o instantâneo inicial é gerado, mesmo se não houver nenhuma assinatura. As alterações registradas são usadas quando um cliente está usando o backup para adicionar um novo nó par. Depois que o backup é restaurado, o par está sincronizado com todas as outras alterações que ocorrem após o backup foi feito. Como os comandos são rastreados no banco de dados de distribuição, a lógica de sincronização pode examinar o último backup LSN e usar isso como um ponto de partida, sabendo que o comando está disponível se o backup foi feito dentro do período de retenção máximo. (O valor padrão para o período de retenção mínimo é o período de retenção 0 horas e o máximo é 24 horas.)  
  
 Quando a sincronização imediata for desativada, as alterações são mantidas pelo menos o período de retenção mínimo e limpas imediatamente para todas as transações que já são replicadas. Se a sincronização imediata for desativada e estiver configurada com o período de retenção padrão, provavelmente as alterações necessárias após a realização do backup foram limpas, e novo nó par não será inicializado corretamente. A única opção restante é a confirmação da topologia. A ativação da sincronização imediata oferece maior flexibilidade e é a configuração recomendada para a replicação P2P.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_changepublication**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
