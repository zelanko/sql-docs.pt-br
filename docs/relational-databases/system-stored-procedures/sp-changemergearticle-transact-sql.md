---
title: sp_changemergearticle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/09/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c2b4b07b79b061b85e50cd51c4716173f073a6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um artigo de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação na qual o artigo existe. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo a ser alterado. *artigo* é **sysname**, sem padrão.  
  
 [  **@property=**] **'***propriedade***'**  
 É a propriedade a ser alterada para um determinado artigo e publicação. *propriedade* é **nvarchar (30)**, e pode ser um dos valores listado na tabela.  
  
 [  **@value=**] **'***valor***'**  
 É o novo valor da propriedade especificada. *valor* é **nvarchar (1000)**, e pode ser um dos valores listado na tabela.  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valores|Description|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|Habilita o uso de um resolvedor interativo para o artigo.|  
||**false**|Desabilita o uso de um resolvedor interativo para o artigo.|  
|**article_resolver**||Resolvedor personalizado para o artigo. Aplica-se somente a um artigo de tabela.|  
|**check_permissions** (bitmap)|**0x00**|Permissões em nível de tabela não são verificadas.|  
||**0x10**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções INSERT feitas no Assinante sejam aplicadas no Publicador.|  
||**0x20**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções UPDATE feitas no Assinante sejam aplicadas no Publicador.|  
||**0x40**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções DELETE feitas no Assinante sejam aplicadas no Publicador.|  
|**column_tracking**|**true**|Ativa o rastreamento em nível de coluna. Aplica-se somente a um artigo de tabela.<br /><br /> Observação: O rastreamento em nível de coluna não pode ser usado ao publicar tabelas com mais de 246 colunas.|  
||**false**|Ativa o rastreamento em nível de coluna e deixa a detecção de conflito no nível de linha. Aplica-se somente a um artigo de tabela.|  
|**compensate_for_errors**|**true**|Ações de compensação são executadas quando ocorrem erros durante a sincronização. Para obter mais informações, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
||**false**|As ações de compensação não são executadas, o que é o comportamento padrão. Para obter mais informações, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).<br /><br /> **\*\*Importante \* \***  Embora os dados nas linhas afetadas pareçam estar fora de convergência, assim que você resolva os erros, as alterações podem ser aplicadas e dados convergidos. Se a tabela de origem para um artigo já estiver publicada em outra publicação, em seguida, o valor de *compensate_for_errors* devem ser as mesmas para os dois artigos.|  
|**creation_script**||Caminho e nome de um script de esquema de artigo opcional usados para criar o artigo no banco de dados de assinatura.|  
|**delete_tracking**|**true**|Instruções DELETE são replicadas, o que é o comportamento padrão.|  
||**false**|Instruções DELETE não são replicadas.<br /><br /> **\*\*Importante \* \***  configuração **delete_tracking** para **false** resulta em não convergência e as linhas excluídas precisa ser removidos manualmente.|  
|**Descrição**||Entrada descritiva para o artigo.|  
|**destination_owner**||Nome do proprietário do objeto de banco de dados de assinatura, se não **dbo**.|  
|**identity_range**||**bigint** que especifica o tamanho do intervalo a ser usado ao atribuir novos valores de identidade, se o artigo tiver **identityrangemanagementoption** definida como **automática** ou **auto_identity_ intervalo** definida como **true**. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "Replicação de mesclagem" [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identityrangemanagementoption**|**Manual**|Desabilita gerenciamento automático do intervalo de identidade. Marca colunas de identidade com NOT FOR REPLICATION para ativar o tratamento manual do intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
||**Nenhum**|Desabilita todo o gerenciamento do intervalo de identidade.|  
|**logical_record_level_conflict_detection**|**true**|Um conflito será detectado se forem feitas alterações no registro lógico. Requer que **logical_record_level_conflict_resolution** ser definido como **true**.|  
||**false**|Detecção de conflito padrão é usada conforme especificado por **column_tracking**.|  
|**logical_record_level_conflict_resolution**|**true**|Todo o registro lógico vencedor substitui o registro lógico perdedor.|  
||**false**|As linhas vencedoras não são restringidas ao registro lógico.|  
|**partition_options**|**0**|A filtragem do artigo é estática ou não gera um subconjunto único de dados para cada partição, ou seja, uma partição “sobreposta”.|  
||**1**|As partições são sobrepostas e as atualizações DML feitas no Assinante não podem alterar a partição a qual uma linha pertence.|  
||**2**|A filtragem do artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.|  
||**3**|A filtragem para o artigo gera partições não sobrepostas exclusivas de cada assinatura.<br /><br /> Observação: Se você especificar um valor de **3** para **partition_options**, pode haver apenas uma única assinatura para cada partição de dados nesse artigo. Se uma segunda assinatura for criada na qual o critério de filtragem da nova assinatura for resolvido para a mesma partição como a assinatura existente, a assinatura existente será cancelada.|  
|**pre_creation_command**|**Nenhum**|Se a tabela já existir no Assinante, nenhuma ação será tomada.|  
||**Excluir**|Emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.|  
||**drop**|Cancela a tabela antes de recriá-la.|  
||**Truncar**|Trunca a tabela de destino.|  
|**processing_order**||**int** que indica a ordem de processamento de artigos em uma publicação de mesclagem.|  
|**pub_identity_range**||**bigint** que especifica o tamanho do intervalo alocado a um assinante com assinatura de servidor, se o artigo tiver **identityrangemanagementoption** definida como **automática** ou **automática _identity_range** definida como **true**. Esse intervalo de identidade é reservado para um Assinante de republicação para ser alocado a seus próprios Assinantes. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "Replicação de mesclagem" [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**published_in_tran_pub**|**true**|Artigo também é publicado em uma publicação transacional.|  
||**false**|O artigo também não é publicado em uma publicação transacional.|  
|**resolver_info**||É usado para especificar informações adicionais requeridas por um determinador personalizado. Alguns resolvedores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] necessitam de uma coluna fornecida como entrada para o resolvedor. **resolver_info** é **nvarchar (255)**, com um padrão NULL. Para obter mais informações, consulte [Resolvedores Microsoft baseados em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).|  
|**schema_option** (bitmap)||Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.|  
||**0x00**|Desabilita a execução de script pelo Snapshot Agent e usa o script fornecido **creation_script**.|  
||**0x01**|Gera o script de criação de objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante).|  
||**0x10**|Gera um índice clusterizado correspondente.|  
||**0x20**|Converte tipos de dados definidos pelo usuário em tipos de dados base no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT (tipo definido pelo usuário), se uma coluna UDT fizer parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT.|  
||**0x40**|Gera índices não clusterizados correspondentes.|  
||**0x80**|Inclui integridade referencial declarada nas chaves primárias.|  
||**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
||**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
||**0x400**|Replica restrições CHECK.|  
||**0x800**|Replica padrões.|  
||**0x1000**|Replica agrupamento em nível de coluna.|  
||**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
||**0x4000**|Replica chaves exclusivas definidas em um artigo de tabela.|  
||**0x8000**|Gera instruções ALTER TABLE em scripts de restrições.|  
||**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
||**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
||**0x100000**|Replica o esquema de partição para um índice particionado.|  
||**0x200000**|Replica estatísticas de tabela.|  
||**0x400000**|Replica associações padrão|  
||**0x800000**|Replica associações de regra.|  
||**0x1000000**|Replica o índice de texto completo.|  
||**0x2000000**|Coleções de esquemas XML associada a **xml** colunas não são replicadas.|  
||**0x4000000**|Replica índices em **xml** colunas.|  
||**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
||**0x10000000**|Converte **xml** colunas **ntext** no assinante.|  
||**0x20000000**|Converte tipos de dados objeto grande (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) que foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de dados que têm suporte em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0x40000000**|Replica permissões.|  
||**0x80000000**|Tentativa de remover dependências de todos os objetos que não fazem parte da publicação.|  
||**0x100000000**|Use esta opção para replicar o atributo FILESTREAM, se for especificado em **varbinary (max)** colunas. Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicação de tabelas com colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes não tem suporte, independentemente de como essa opção de esquema é definida. Consulte a opção relacionada **0x800000000**.|  
||**0x200000000**|Converte tipos de dados de data e hora (**data**, **tempo**, **datetimeoffset**, e **datetime2**) que foram introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para tipos de dados que têm suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar Scripts antes e após a aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
||**0x1000000000**|Converte tipos common language runtime (CLR) definidos pelo usuário (UDTs) em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Converte o **hierarchyid** tipo de dados **varbinary (max)** para que colunas do tipo **hierarchyid** podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar **hierarchyid** colunas em tabelas replicadas, consulte [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Converte o **geografia** e **geometria** para tipos de dados **varbinary (max)** para que colunas desses tipos podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Replica índices em colunas do tipo **geografia** e **geometria**.|  
||NULL|O sistema gera automaticamente uma opção de esquema válida para o artigo.|  
|**status**|**ativo**|O script de processamento inicial para publicação da tabela é executado.|  
||**unsynced**|O script de processamento inicial para publicar a tabela é executado da próxima vez que o Snapshot Agent é executado.|  
|**stream_blob_columns**|**true**|Uma otimização de fluxo de dados é usada ao replicar colunas de objeto binário grande. Porém, certas funcionalidades de replicação de mesclagem, como registros lógicos, ainda podem impedir que a otimização de fluxo seja usada. *stream_blob_columns* é definida como true quando FILESTREAM está habilitado. Isso permite a replicação de dados FILESTREAM para executar da maneira ideal e reduzir a utilização de memória. Para forçar os artigos de tabela FILESTREAM a não usarem o fluxo de blob, defina *stream_blob_columns* como false.<br /><br /> **\*\*Importante \* \***  habilitação dessa otimização de memória pode prejudicar o desempenho do Merge Agent durante a sincronização. Esta opção só deve ser usada ao replicar colunas que contêm megabytes de dados.|  
||**false**|A otimização não é usada ao replicar colunas de objeto binário grande.|  
|**subscriber_upload_options**|**0**|Nenhuma restrição em atualizações feitas em um Assinante com uma assinatura de cliente. As alterações são carregadas no Publicador. A alteração dessa propriedade pode exigir a reinicialização dos Assinantes existentes.|  
||**1**|Alterações são permitidas em um Assinante com assinatura de cliente, mas elas não são carregadas no Publicador.|  
||**2**|Não são permitidas alterações em um Assinante com uma assinatura de cliente.|  
|**subset_filterclause**||Cláusula WHERE especificando filtragem horizontal. Aplica-se somente a um artigo de tabela.<br /><br /> **\*\*Importante \* \***  por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor HOST_NAME, talvez você precise converter tipos de dados usando [converter](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre as práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME ()" em [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
|**limite**||Valor de porcentagem usado por assinantes que executam [!INCLUDE[ssEW](../../includes/ssew-md.md)] ou versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **limite** controla quando o Merge Agent atribui um novo intervalo de identidade. Quando a porcentagem de valores especificada no limite é usada, o Merge Agent cria um novo intervalo de identidade. Usado quando **identityrangemanagementoption** é definido como **automática** ou **auto_identity_range** é definido como **true**. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "Replicação de mesclagem" [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**1**|A assinatura digital em um resolvedor personalizado é verificada para determinar se é de uma fonte confiável.|  
||**0**|A assinatura digital em um resolvedor personalizado não é verificada para determinar se é de uma fonte confiável.|  
|NULL (padrão)||Retorna a lista de valores com suporte para *propriedade*.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo de mesclagem fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem podem invalidar o instantâneo inválido, e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
 Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo de mesclagem fazem com que a assinatura ser reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem fazer com que as assinaturas existentes sejam reinicializadas e dá permissão para que ocorra a reinicialização da assinatura.  
  
 Consulte a seção Comentários para as propriedades que, quando alteradas, requerem que todas as assinaturas existentes sejam reiniciadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergearticle** é usado em replicação de mesclagem.  
  
 Porque **sp_changemergearticle** é usado para alterar as propriedades de artigo especificadas inicialmente usando [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para obter informações adicionais sobre essas propriedades.  
  
 Alterando as propriedades seguintes requer que um novo instantâneo seja gerado, e você deve especificar um valor de **1** para o *force_invalidate_snapshot* parâmetro:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 Alterando as propriedades seguintes requer existentes assinaturas sejam reinicializadas e você deve especificar um valor de **1** para o *force_reinit_subscription* parâmetro:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 Ao especificar um valor de 3 para **partition_options**, metadados são limpos sempre que o Merge Agent é executado e o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere habilitar o instantâneo particionado solicitado pelo assinante. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Ao definir o **column_tracking** propriedade, se a tabela já estiver publicada em outras publicações de mesclagem, a coluna de rastreamento deve ser o mesmo que o valor que está sendo usado por artigos existentes com base nessa tabela. Esse parâmetro só é específico a artigos de tabela.  
  
 Se várias publicações publicarem artigos com base na mesma tabela subjacente, alterando o **delete_tracking** propriedade ou o **compensate_for_errors** para um artigo faz com que a mesma alteração em fazer os outros artigos que são baseados na mesma tabela.  
  
 Se o logon/conta de usuário do Publicador usado pelo processo de mesclagem não possuir as permissões corretas de tabela, as alterações inválidas serão registradas como conflitos.  
  
 Ao alterar o valor de **schema_option**, o sistema não executará uma atualização bit a bit. Isso significa que quando você definir **schema_option** usando **sp_changemergearticle**existente configurações de bit poderão ser desativadas. Para manter as configurações existentes, você deve executar [& (AND bit a bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) entre o valor que você está definindo o e o valor atual de *schema_option*, que pode ser determinado executando [sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md).  
  
> [!CAUTION]  
>  Quando você muitas (talvez centenas) de artigos em uma publicação e você executar **sp_changemergearticle** para um dos artigos, pode levar muito tempo para concluir a execução.  
  
## <a name="valid-schema-option-table"></a>Tabela de opção de esquema válida  
 A tabela a seguir descreve permitidos *schema_option*valores, dependendo do tipo de artigo.  
  
|Tipo de artigo|Valores de opção de esquema|  
|------------------|--------------------------|  
|**somente esquema de função**|**0x01** e **0x2000**|  
|**somente o esquema de exibição indexada**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
|**somente esquema de PROC**|**0x01** e **0x2000**|  
|**table**|Todas as opções.|  
|**somente o esquema de exibição**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_changemergearticle**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
