---
title: SP_CHANGEARTICLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords: sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
caps.latest.revision: "77"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26e758e6f4884309a17d5abfaa82b64d767d4df5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um artigo em uma publicação transacional ou de instantâneo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação que contém o artigo. *publicação* é **sysname**, com um padrão NULL.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo cuja propriedade deve ser alterada. *artigo* é **sysname**, com um padrão NULL.  
  
 [  **@property=**] **'***propriedade***'**  
 É uma propriedade de artigo a ser alterada. *propriedade* é **nvarchar (100)**.  
  
 [  **@value=**] **'***valor***'**  
 É o valor novo da propriedade de artigo. *valor* é **nvarchar (255)**.  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valores|Description|  
|--------------|------------|-----------------|  
|**creation_script**||Caminho e nome de um script de esquema de artigo usados para criar tabelas de destino. O padrão é NULO.|  
|**del_cmd**||Instrução DELETE a ser executada; caso contrário, será construída do log.|  
|**Descrição**||Nova entrada descritiva para o artigo.|  
|**dest_object**||Fornecido para compatibilidade com versões anteriores. Use **dest_table**.|  
|**dest_table**||Nova tabela de destino.|  
|**destination_owner**||Nome do proprietário do objeto de destino.|  
|**filtro**||Novo procedimento armazenado a ser usado para filtrar a tabela (filtragem horizontal). O padrão é NULO. Não pode ser alterado para publicações em replicação ponto a ponto.|  
|**fire_triggers_on_snapshot**|**true**|Gatilhos de usuário replicados são executados quando o instantâneo inicial é aplicado.<br /><br /> Observação: para gatilhos a serem replicados, o valor de máscara de bits de *schema_option* deve incluir o valor **0x100**.|  
||**false**|Gatilhos de usuário replicados não são executados quando o instantâneo inicial é aplicado.|  
|**identity_range**||Controla o tamanho de intervalos de identidade atribuídos atribuído ao Assinante. Sem suporte para replicação ponto a ponto.|  
|**ins_cmd**||Instrução INSERT a ser executada; caso contrário, será construída do log.|  
|**pre_creation_cmd**||Comando de pré-criação que pode descartar, excluir ou truncar a tabela de destino antes que a sincronização seja aplicada.|  
||**Nenhum**|Não usa um comando.|  
||**drop**|Descarta a tabela de destino.|  
||**Excluir**|Exclui a tabela de destino.|  
||**Truncar**|Trunca a tabela de destino.|  
|**pub_identity_range**||Controla o tamanho de intervalos de identidade atribuídos atribuído ao Assinante. Sem suporte para replicação ponto a ponto.|  
|**schema_option**||Especifica o bitmap da opção de geração de esquema para o artigo determinado. *schema_option* é **binary (8)**. Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.|  
||**0x00**|Desabilita execução de script pelo Agente de Instantâneo.|  
||**0x01**|Gera a criação do objeto (CREATE TABLE, CREATE PROCEDURE, e assim por diante).|  
||**0x02**|Gera os procedimentos armazenados que propagam alterações para o artigo, se definido.|  
||**0x04**|Os scripts das colunas de identidade são executados com a propriedade IDENTITY.|  
||**0x08**|Replicar **timestamp** colunas. Se não for definido, **timestamp** colunas são replicadas como **binário**.|  
||**0x10**|Gera um índice clusterizado correspondente.|  
||**0x20**|Converte UDTs (tipos de dados definidos pelo usuário) em tipos de dados básicos no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT, se uma coluna UDT for parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT. Sem suporte para Publicadores Oracle.|  
||**0x40**|Gera índices não clusterizados correspondentes.|  
||**0x80**|Inclui integridade referencial declarada nas chaves primárias.|  
||**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
||**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
||**0x400**|Replica restrições CHECK.|  
||**0x800**|Replica padrões.|  
||**0x1000**|Replica agrupamento em nível de coluna.|  
||**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
||**0x4000**|Replica chaves exclusivas definidas em um artigo de tabela.|  
||**0x8000**|Reproduz chave primária e chaves exclusivas em um artigo de tabela como restrições usando instruções ALTER TABLE.<br /><br /> Observação: Essa opção foi preterida. Use **0x80** e **0x4000** em vez disso.|  
||**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
||**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
||**0x100000**|Replica o esquema de partição para um índice particionado.|  
||**0x200000**|Replica estatísticas de tabela.|  
||**0x400000**|Associações padrão|  
||**0x800000**|Associações de regra|  
||**0x1000000**|Índice de texto completo|  
||**0x2000000**|Coleções de esquemas XML associada a **xml** colunas não são replicadas.|  
||**0x4000000**|Replica índices em **xml** colunas.|  
||**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
||**0x10000000**|Converte **xml** colunas **ntext** no assinante.|  
||**0x20000000**|Converte tipos de dados objeto grande (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) que foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de dados que têm suporte em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0x40000000**|Replica permissões.|  
||**0x80000000**|Tentativa de remover dependências de todos os objetos que não fazem parte da publicação.|  
||**0x100000000**|Use esta opção para replicar o atributo FILESTREAM, se for especificado em **varbinary (max)** colunas. Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicação de tabelas com colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes não tem suporte, independentemente de como essa opção de esquema é definida.<br /><br /> Consulte a opção relacionada **0x800000000**.|  
||**0x200000000**|Converte tipos de dados de data e hora (**data**, **tempo**, **datetimeoffset**, e **datetime2**) que foram introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para tipos de dados que têm suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar Scripts antes e após a aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
||**0x1000000000**|Converte tipos common language runtime (CLR) definidos pelo usuário (UDTs) maiores que 8000 bytes em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Converte o **hierarchyid** tipo de dados **varbinary (max)** para que colunas do tipo **hierarchyid** podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações sobre como usar **hierarchyid** colunas em tabelas replicadas, consulte [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Converte o **geografia** e **geometria** para tipos de dados **varbinary (max)** para que colunas desses tipos podem ser replicadas para assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Replica índices em colunas do tipo **geografia** e **geometria**.|  
||**0x20000000000**|Replica o atributo SPARSE para colunas. Para obter mais informações sobre esse atributo, consulte [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|  
||**0x40000000000**|Habilite o script pelo snapshot agent para criar a tabela com otimização de memória no assinante.|  
||**0x80000000000**|Converte um índice clusterizado em índice não clusterizado para artigos com otimização de memória.|  
|**status**||Especifica o novo status da propriedade.|  
||**partições horizontais DTS**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**incluir nomes de coluna**|Nomes de coluna são incluídos na instrução INSERT replicada.|  
||**Não há nomes de coluna**|Nomes de coluna não são incluídos na instrução INSERT replicada.|  
||**sem partições horizontais dts**|A partição horizontal para o artigo não é definida por uma assinatura transformável.|  
||**Nenhum**|Limpa todas as opções de status no [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) de tabela e marca o artigo como inativo.|  
||**parâmetros**|As alterações são propagadas ao Assinante usando comandos com parâmetros. Essa é a configuração padrão para um novo artigo.|  
||**literais de cadeia de caracteres**|As alterações são propagadas ao Assinante usando valores de literal de cadeia de caracteres.|  
|**sync_object**||Nome da tabela ou exibição usado para produzir um arquivo de saída de sincronização. O padrão é NULO. Sem suporte para Publicadores Oracle.|  
|**espaço de tabela**||Identifica o espaço de tabela usado pela tabela de log para um artigo publicado de um banco de dados de Oracle. Para obter mais informações, consulte [Gerenciar espaços de tabela Oracle](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md).|  
|**limite**||Valor percentual para controle quando o Distribution Agent atribuir um novo intervalo de identidade. Sem suporte para replicação ponto a ponto.|  
|**tipo**||Sem suporte para Publicadores Oracle.|  
||**logbased**|Artigo com base em log.|  
||**logbased manualboth**|Artigo com base em log com filtro manual e exibição manual. Essa opção requer que o *sync_object* e *filtro* propriedades também ser definidas. Sem suporte para Publicadores Oracle.|  
||**logbased manualfilter**|Artigo com base em log com filtro manual. Essa opção requer que o *sync_object* e *filtro* propriedades também ser definidas. Sem suporte para Publicadores Oracle.|  
||**logbased manualview**|Artigo com base em log com exibição manual. Essa opção requer que o *sync_object* propriedade também seja definida. Sem suporte para Publicadores Oracle.|  
||**viewlogbased indexado**|Artigo de exibição indexada com base em log. Sem suporte para Publicadores Oracle. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente.|  
||**manualboth viewlogbased indexada**|Artigo de exibição indexada com filtro manual e exibição manual. Essa opção requer que o *sync_object* e *filtro* propriedades também ser definidas. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
||**manualfilter viewlogbased indexada**|Artigo de exibição indexada com filtro manual. Essa opção requer o *sync_object* e *filtro* propriedades também ser definidas. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
||**manualview viewlogbased indexada**|Artigo de exibição indexada com base em log com exibição manual. Essa opção requer que o *sync_object* propriedade também seja definida. Para este tipo de artigo, a tabela base não precisa ser publicada separadamente. Sem suporte para Publicadores Oracle.|  
|**upd_cmd**||Instrução UPADTE a ser executada; caso contrário, será construída do log.|  
|NULL|NULL|Retorna uma lista de propriedades de artigo que podem ser alteradas.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo inválido e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
 Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
 [  **@force_reinit_subscription=]***force_reinit_subscription*  
 Confirma que a ação tomada por esse procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit** com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que a assinatura ser reiniciada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo fazem com que as assinaturas existentes sejam reinicializadas e dá permissão para que ocorra a reinicialização da assinatura.  
  
 Consulte a seção Comentários para as propriedades que, quando alteradas, requerem que todas as assinaturas existentes sejam reiniciadas.  
  
 [  **@publisher** =] **'***publicador***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado ao alterar as propriedades de artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **SP_CHANGEARTICLE** é usado em replicação de instantâneo e replicação transacional.  
  
 Quando um artigo pertence a uma publicação que oferece suporte à replicação transacional ponto a ponto, você só pode alterar o **descrição**, **ins_cmd**, **upd_cmd**e **del_cmd** propriedades.  
  
 Alterar qualquer uma das propriedades seguintes requer que um novo instantâneo seja gerado, e você deve especificar um valor de **1** para o *force_invalidate_snapshot* parâmetro:  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 Alterar qualquer uma das propriedades seguintes requer existentes assinaturas sejam reinicializadas e você deve especificar um valor de **1** para o *force_reinit_subscription* parâmetro.  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **filtro**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 Dentro de uma publicação existente, você pode usar **sp_changearticle** para alterar um artigo, sem a necessidade de descartar e recriar a publicação inteira.  
  
> [!NOTE]  
>  Ao alterar o valor de *schema_option*, o sistema não executará uma atualização bit a bit. Isso significa que quando você definir *schema_option* usando **sp_changearticle**existente configurações de bit poderão ser desativadas. Para manter as configurações existentes, você deve executar [& (AND bit a bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) entre o valor que você está definindo o e o valor atual de *schema_option*, que pode ser determinado executando [sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md).  
  
## <a name="valid-schema-options"></a>Opções de esquema válidas  
 A tabela a seguir descreve os valores permitidos de *schema_option* com base no tipo de replicação (mostrados na parte superior) e o tipo de artigo (mostrado abaixo da primeira coluna).  
  
|Tipo de artigo|Tipo de replicação||  
|------------------|----------------------|------|  
||Transacional.|Instantâneo|  
|**logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased manualfilter**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbased manualview**|Todas as opções|Todas as opções, mas **0x02**|  
|**modo de exibição indexado logbase manualboth**|Todas as opções|Todas as opções, mas **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**Serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente esquema de PROC**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente o esquema de exibição**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
|**somente esquema de função**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**somente o esquema de exibição indexada**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
  
> [!NOTE]  
>  Para publicações de atualização enfileiradas, o *schema_option* valor **0x80** deve ser habilitado. Com o suporte *schema_option* valores não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações são: **0x01**, **0x02**, **0x10**,  **0x40**, **0x80**, **0x1000** e **0x4000**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_changearticle**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
