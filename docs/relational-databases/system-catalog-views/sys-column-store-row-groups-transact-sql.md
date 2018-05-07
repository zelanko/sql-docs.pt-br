---
title: column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ef19c029232369de3a2da590e17f97a8bdb13655
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syscolumnstorerowgroups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Fornece informações do índice columnstore clusterizado por segmento para ajudar o administrador a tomar decisões de gerenciamento de sistema. **column_store_row_groups** tem uma coluna para o número total de linhas armazenadas fisicamente (inclusive as marcadas como excluídas) e uma coluna para o número de linhas marcadas como excluídas. Use **column_store_row_groups** para determinar qual linha grupos têm uma alta porcentagem de linhas excluídas em devem ser recriados.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|A ID da tabela na qual esse índice é definido.|  
|**index_id**|**Int**|ID do índice para a tabela que contém esse índice columnstore.|  
|**partition_number**|**Int**|ID da partição da tabela que contém o row_group_id do grupo de linhas. Você pode usar o partition_number para adicionar esse DMV a sys.partitions.|  
|**row_group_id**|**Int**|O número do grupo de linhas associado a esse grupo de linhas. Isso é exclusivo dentro da partição.<br /><br /> -1 = final de uma tabela na memória.|  
|**delta_store_hobt_id**|**bigint**|O hobt_id para o grupo de linhas aberto no repositório delta.<br /><br /> NULL se o grupo de linhas não está no repositório delta.<br /><br /> NULL para o final de uma tabela na memória.|  
|**state**|**tinyint**|O número de ID associado a state_description.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED <br /><br /> 4 = DA MARCA DE EXCLUSÃO|  
|**state_description**|**nvarchar(60)**|Descrição do estado persistente do grupo de linhas:<br /><br /> INVISIBLE – um segmento compactado oculto no processo de ter sido criado a partir dos dados em um repositório delta. As ações de leitura usarão o repositório delta até que o segmento compactado invisível seja concluído. Em seguida, o novo segmento é tornado visível e o repositório delta da origem é removido.<br /><br /> OPEN – Um grupo de linhas de leitura/gravação que está aceitando novos registros. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> CLOSED – Um grupo de linhas que foi preenchido, mas ainda não compactado pelo processo Tuple Mover.<br /><br /> COMPRESSED – Um grupo de linhas que foi preenchido e compactado.|  
|**total_rows**|**bigint**|Total de linhas fisicamente armazenadas no grupo de linhas. Algumas podem ter sido excluídas, mas ainda estão armazenadas. O número máximo de linhas em um grupo de linhas é 1.048.576 (FFFFF hexadecimal).|  
|**deleted_rows**|**bigint**|Total de linhas no grupo de linhas marcadas como excluídas. Isso é sempre 0 para grupos de linhas DELTA.|  
|**size_in_bytes**|**bigint**|Tamanho em bytes de todos os dados nesse grupo de linhas (que não inclui metadados ou dicionários compartilhados), para rowgroups DELTA e COLUMNSTORE.|  
  
## <a name="remarks"></a>Remarks  
 Retorna uma linha para cada grupo de linhas columnstore para cada tabela que tem um índice columnstore clusterizado ou não clusterizado.  
  
 Use **column_store_row_groups** para determinar o número de linhas incluídas no grupo de linhas e o tamanho do grupo de linhas.  
  
 Quando o número de linhas excluídas em um grupo de linhas cresce para uma grande porcentagem do total de linhas, a tabela fica menos eficiente. Recrie o índice columnstore para reduzir o tamanho da tabela, reduzindo a E/S de disco necessária para ler a tabela. Para recriar o índice columnstore, use o **RECRIAR** opção do **ALTER INDEX** instrução.  
  
 O columnstore atualizável primeiro insere novos dados em um **abrir** rowgroup, que está no formato rowstore e às vezes também é conhecido como uma tabela delta.  Quando um rowgroup aberto está cheio, seu estado é alterado para **fechado**. Um rowgroup fechado é compactado no formato columnstore pelo tuple mover e o estado muda para **COMPRESSED**.  O Tuple Mover é um processo em segundo plano que periodicamente é acionado e verifica se há algum rowgroup fechado que já esteja pronto para compactar em um rowgroup columnstore.  O Tuple Mover também desaloca todos os rowgroups nos quais cada linha foi excluída. Rowgroups desalocados são marcados como **TOMBSTONE**. Para executar o tuple mover imediatamente, use o **REORGANIZAR** opção do **ALTER INDEX** instrução.  
  
 Quando um grupo de linhas de columnstore tiver sido preenchido, ele é compactado e para de aceitar novas linhas. Quando as linhas são excluídas de um grupo compactado, elas permanecem, mas são marcadas como excluídas. As atualizações para um grupo compactado são implementadas como uma exclusão do grupo compactado, e uma inserção em um grupo aberto.  
  
## <a name="permissions"></a>Permissões  
 Retorna informações de uma tabela, se o usuário tiver **VIEW DEFINITION** permissão na tabela.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 A exemplo a seguir adiciona o **column_store_row_groups** tabela a outras tabelas do sistema para retornar informações sobre tabelas específicas. A coluna calculada `PercentFull` é uma estimativa da eficiência do grupo de linhas. Para localizar informações em uma única tabela, remova os hífens de comentário na frente do **onde** cláusula e forneça um nome de tabela.  
  
```  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

