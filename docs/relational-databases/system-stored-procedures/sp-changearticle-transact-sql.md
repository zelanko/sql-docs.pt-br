---
title: sp_changearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0f9b47d2a8d5732aa42ed92f2b5af00524052e6
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977526"
---
# <a name="sp_changearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera as propriedades de um artigo em uma publicação transacional ou de instantâneo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. a *publicação* é **sysname**, com um padrão de NULL.  
  
`[ @article = ] 'article'`É o nome do artigo cuja propriedade deve ser alterada. o *artigo* é **sysname**, com um padrão de NULL.  
  
`[ @property = ] 'property'`É uma propriedade de artigo a ser alterada. a *Propriedade* é **nvarchar (100)**.  
  
`[ @value = ] 'value'`É o novo valor da Propriedade do artigo. o *valor* é **nvarchar (255)**.  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valores|Descrição|  
|--------------|------------|-----------------|  
|**creation_script**||Caminho e nome de um script de esquema de artigo usados para criar tabelas de destino. O padrão é NULO.|  
|**del_cmd**||Instrução DELETE a ser executada; caso contrário, será construída do log.|  
|**descrição**||Nova entrada descritiva para o artigo.|  
|**dest_object**||Fornecido para compatibilidade com versões anteriores. Use **dest_table**.|  
|**dest_table**||Nova tabela de destino.|  
|**destination_owner**||Nome do proprietário do objeto de destino.|  
|**sem**||Novo procedimento armazenado a ser usado para filtrar a tabela (filtragem horizontal). O padrão é NULO. Não pode ser alterado para publicações em replicação ponto a ponto.|  
|**fire_triggers_on_snapshot**|**true**|Gatilhos de usuário replicados são executados quando o instantâneo inicial é aplicado.<br /><br /> Observação: para que os gatilhos sejam replicados, o valor de bitmask de *schema_option* deve incluir o valor **0x100**.|  
||**false**|Gatilhos de usuário replicados não são executados quando o instantâneo inicial é aplicado.|  
|**identity_range**||Controla o tamanho de intervalos de identidade atribuídos atribuído ao Assinante. Sem suporte para replicação ponto a ponto.|  
|**ins_cmd**||Instrução INSERT a ser executada; caso contrário, será construída do log.|  
|**pre_creation_cmd**||Comando de pré-criação que pode descartar, excluir ou truncar a tabela de destino antes que a sincronização seja aplicada.|  
||**nenhum**|Não usa um comando.|  
||**suspensa**|Descarta a tabela de destino.|  
||**delete**|Exclui a tabela de destino.|  
||**truncar**|Trunca a tabela de destino.|  
|**pub_identity_range**||Controla o tamanho de intervalos de identidade atribuídos atribuído ao Assinante. Sem suporte para replicação ponto a ponto.|  
|**schema_option**||Especifica o bitmap da opção de geração de esquema para o artigo determinado. *schema_option* é **binary (8)**. Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.|  
||**0x00**|Desabilita execução de script pelo Agente de Instantâneo.|  
||**0x01**|Gera a criação do objeto (CREATE TABLE, CREATE PROCEDURE, e assim por diante).|  
||**0x02**|Gera os procedimentos armazenados que propagam alterações para o artigo, se definido.|  
||**0x04**|Os scripts das colunas de identidade são executados com a propriedade IDENTITY.|  
||**0x08**|Replicar colunas **timestamp** . Se não for definido, as colunas de **carimbo de data/hora** serão replicadas como **binários**.|  
||**0x10**|Gera um índice clusterizado correspondente.|  
||**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT. Sem suporte para Publicadores Oracle.|  
||**0x40**|Gera índices não clusterizados correspondentes.|  
||**0x80**|Inclui integridade referencial declarada nas chaves primárias.|  
||**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
||**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
||**0x400**|Replica restrições CHECK.|  
||**0x800**|Replica padrões.|  
||**0x1000**|Replica ordenação em nível de coluna.|  
||**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
||**0x4000**|Replica chaves exclusivas definidas em um artigo de tabela.|  
||**0x8000**|Reproduz chave primária e chaves exclusivas em um artigo de tabela como restrições usando instruções ALTER TABLE.<br /><br /> Observação: essa opção foi preterida. Em vez disso, use **0x80** e **0x4000** .|  
||**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
||**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
||**0x100000**|Replica o esquema de partição para um índice particionado.|  
||**0x200000**|Replica estatísticas de tabela.|  
||**0x400000**|Associações padrão|  
||**0x800000**|Associações de regra|  
||**0x1000000**|Índice de texto completo|  
||**0x2000000**|As coleções de esquema XML vinculadas a colunas **XML** não são replicadas.|  
||**0x4000000**|Replica índices em colunas **XML** .|  
||**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
||**0x10000000**|Converte colunas **XML** em **ntext** no Assinante.|  
||**0x20000000**|Converte tipos de dados de objeto grande (**nvarchar (max)**, **varchar (max)** e **varbinary (max)**) que foram introduzidos nos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tipos de dados com suporte no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] .|  
||**0x40000000**|Replicar permissões.|  
||**0x80000000**|Tente descartar as dependências de todos os objetos que não fazem parte da publicação.|  
||**0x100000000**|Use esta opção para replicar o atributo FILESTREAM se ele for especificado em colunas **varbinary (max)** . Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Não há suporte para a replicação de tabelas que têm colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes, independentemente de como essa opção de esquema está definida.<br /><br /> Consulte a opção relacionada **0x800000000**.|  
||**0x200000000**|Converte os tipos de dados de data e hora (**Date**, **time**, **DateTimeOffset**e **datetime2**) que foram introduzidos nos [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tipos de dados com suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
||**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar scripts antes e depois que o instantâneo for aplicado](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
||**0x1000000000**|Converte os UDTs (tipos definidos pelo usuário) Common Language Runtime (CLR) com mais de 8000 bytes em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
||**0x2000000000**|Converte o tipo de dados **hierarchyid** em **varbinary (max)** para que as colunas do tipo **hierarchyid** possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para obter mais informações sobre como usar colunas **hierarchyid** em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Converte os tipos de dados **geography** e **Geometry** em **varbinary (max)** para que as colunas desses tipos possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
||**0x10000000000**|Replica índices em colunas do tipo **geography** e **Geometry**.|  
||**0x20000000000**|Replica o atributo SPARSE para colunas. Para obter mais informações sobre esse atributo, consulte [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
||**0x40000000000**|Habilite o script pelo agente de instantâneo para criar a tabela com otimização de memória no Assinante.|  
||**0x80000000000**|Converte o índice clusterizado em índice não clusterizado para artigos com otimização de memória.|  
|**status**||Especifica o novo status da propriedade.|  
||**dts horizontal partitions**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**include column names**|Nomes de coluna são incluídos na instrução INSERT replicada.|  
||**no column names**|Nomes de coluna não são incluídos na instrução INSERT replicada.|  
||**no dts horizontal partitions**|A partição horizontal para o artigo não é definida por uma assinatura transformável.|  
||**nenhum**|Limpa todas as opções de status na tabela [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) e marca o artigo como inativo.|  
||**parameters**|As alterações são propagadas ao Assinante usando comandos com parâmetros. Essa é a configuração padrão para um novo artigo.|  
||**literais de cadeia de caracteres**|As alterações são propagadas ao Assinante usando valores de literal de cadeia de caracteres.|  
|**sync_object**||Nome da tabela ou exibição usado para produzir um arquivo de saída de sincronização. O padrão é NULO. Sem suporte para Publicadores Oracle.|  
|**espaços**||Identifica o espaço de tabela usado pela tabela de log para um artigo publicado de um banco de dados de Oracle. Para obter mais informações, consulte [Gerenciar espaços de tabela Oracle](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md).|  
|**threshold**||Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Sem suporte para replicação ponto a ponto.|  
|**tipo**||Sem suporte para Publicadores Oracle.|  
||**logbased**|Artigo com base em log.|  
||**logbased manualboth**|Artigo com base em log com filtro manual e exibição manual. Essa opção requer que as propriedades *sync_object* e *Filter* também sejam definidas. Sem suporte para Publicadores Oracle.|  
||**logbased manualfilter**|Artigo com base em log com filtro manual. Essa opção requer que as propriedades *sync_object* e *Filter* também sejam definidas. Sem suporte para Publicadores Oracle.|  
||**logbased manualview**|Artigo com base em log com exibição manual. Essa opção requer que a propriedade *sync_object* também seja definida. Sem suporte para Publicadores Oracle.|  
||**viewlogbased indexados**|Artigo de exibição indexada com base em log. Sem suporte para Publicadores Oracle. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente.|  
||**viewlogbased indexado manualboth**|Artigo de exibição indexada com filtro manual e exibição manual. Essa opção requer que as propriedades *sync_object* e *Filter* também sejam definidas. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
||**viewlogbased indexado manualfilter**|Artigo de exibição indexada com filtro manual. Essa opção requer que as propriedades *sync_object* e *Filter* também sejam definidas. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
||**viewlogbased indexado manualview**|Artigo de exibição indexada com base em log com exibição manual. Essa opção requer que a propriedade *sync_object* também seja definida. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**upd_cmd**||Instrução UPADTE a ser executada; caso contrário, será construída do log.|  
|NULO|NULO|Retorna uma lista de propriedades de artigo que podem ser alteradas.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
 Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo fazem com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
 Consulte a seção Comentários para as propriedades que, quando alteradas, requerem que todas as assinaturas existentes sejam reiniciadas.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao alterar as propriedades do artigo em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changearticle** é usado na replicação de instantâneo e na replicação transacional.  
  
 Quando um artigo pertence a uma publicação que dá suporte à replicação transacional ponto a ponto, você só pode alterar as propriedades **Description**, **ins_cmd**, **upd_cmd**e **del_cmd** .  
  
 A alteração de qualquer uma das propriedades a seguir requer que um novo instantâneo seja gerado, e você deve especificar um valor de **1** para o parâmetro *force_invalidate_snapshot* :  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 A alteração de qualquer uma das propriedades a seguir exige que as assinaturas existentes sejam reinicializadas e você deve especificar um valor de **1** para o parâmetro *force_reinit_subscription* .  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **sem**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 Em uma publicação existente, você pode usar **sp_changearticle** para alterar um artigo sem precisar descartar e recriar a publicação inteira.  
  
> [!NOTE]  
>  Ao alterar o valor de *schema_option*, o sistema não executa uma atualização de bit de bits. Isso significa que, quando você definir *schema_option* usando **sp_changearticle**, as configurações de bits existentes poderão ser desativadas. Para manter as configurações existentes, você deve executar [| (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) entre o valor que você está definindo e o valor atual de *schema_option*, que pode ser determinado executando [sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md).  
  
## <a name="valid-schema-options"></a>Opções de esquema válidas  
 A tabela a seguir descreve os valores permitidos de *schema_option* com base no tipo de replicação (mostrado na parte superior) e no tipo de artigo (mostrado na primeira coluna).  
  
| Tipo de artigo | Tipo de replicação-transacional | Tipo de replicação-instantâneo |
| ------------ | -------------------------------- | --------------------------- |
|**logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**indexed view logbase manualboth**|Todas as opções|Todas as opções, mas **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**proc schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|  
|**func schema only**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**e **0x80000000**|  
|**indexed view schema only**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x40000000**e **0x80000000**|  
  
> [!NOTE]
>  Para publicações de atualização em fila, o valor *schema_option* de **0x80** deve ser habilitado. Os valores de *schema_option* com suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações não são **: 0x01**, **0x02**, **0x10**, **0x40**, **0x80**, **0x1000** e **0x4000**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changearticle**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades do artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droparticle](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticlecolumns](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
