---
description: sys.column_store_row_groups (Transact-SQL)
title: sys. column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a7a6f8a54469aa8a87eb02128ef91672ff69ea3c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486450"
---
# <a name="syscolumn_store_row_groups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações do índice columnstore clusterizado por segmento para ajudar o administrador a tomar decisões de gerenciamento de sistema. **Sys. column_store_row_groups** tem uma coluna para o número total de linhas armazenadas fisicamente (incluindo aquelas marcadas como excluídas) e uma coluna para o número de linhas marcadas como excluídas. Use **Sys. column_store_row_groups** para determinar quais grupos de linhas têm uma alta porcentagem de linhas excluídas e devem ser recriados.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|A ID da tabela na qual esse índice é definido.|  
|**index_id**|**int**|ID do índice para a tabela que contém esse índice columnstore.|  
|**partition_number**|**int**|ID da partição da tabela que contém o row_group_id do grupo de linhas. Você pode usar o partition_number para adicionar esse DMV a sys.partitions.|  
|**row_group_id**|**int**|O número do grupo de linhas associado a esse grupo de linhas. Isso é exclusivo dentro da partição.<br /><br /> -1 = cauda de uma tabela na memória.|  
|**delta_store_hobt_id**|**bigint**|O hobt_id para o grupo de linhas aberto no armazenamento Delta.<br /><br /> NULL se o grupo de linhas não estiver no repositório Delta.<br /><br /> NULL para a parte final de uma tabela na memória.|  
|**state**|**tinyint**|O número de ID associado a state_description.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED <br /><br /> 4 = MARCA PARA EXCLUSÃO|  
|**state_description**|**nvarchar(60)**|Descrição do estado persistente do grupo de linhas:<br /><br /> INVISÍVEL-um segmento compactado oculto no processo de criação de dados em um armazenamento Delta. As ações de leitura usarão o repositório delta até que o segmento compactado invisível seja concluído. Em seguida, o novo segmento é tornado visível e o repositório delta da origem é removido.<br /><br /> ABRIR-um grupo de linhas de leitura/gravação que está aceitando novos registros. Um grupo de linhas aberto ainda está no formato rowstore e não foi compactado para o formato columnstore.<br /><br /> CLOSED-um grupo de linhas que foi preenchido, mas ainda não foi compactado pelo processo de movimentação de tupla.<br /><br /> COMPACTado-um grupo de linhas que foi preenchido e compactado.|  
|**total_rows**|**bigint**|Total de linhas fisicamente armazenadas no grupo de linhas. Algumas podem ter sido excluídas, mas ainda estão armazenadas. O número máximo de linhas em um grupo de linhas é 1.048.576 (FFFFF hexadecimal).|  
|**deleted_rows**|**bigint**|Total de linhas no grupo de linhas marcadas como excluídas. Isso é sempre 0 para grupos de linhas DELTA.|  
|**size_in_bytes**|**bigint**|Tamanho em bytes de todos os dados nesse grupo de linhas (que não inclui metadados ou dicionários compartilhados), para rowgroups DELTA e COLUMNSTORE.|  
  
## <a name="remarks"></a>Comentários  
 Retorna uma linha para cada grupo de linhas columnstore para cada tabela que tem um índice columnstore clusterizado ou não clusterizado.  
  
 Use **Sys. column_store_row_groups** para determinar o número de linhas incluídas no grupo de linhas e o tamanho do grupo de linhas.  
  
 Quando o número de linhas excluídas em um grupo de linhas cresce para uma grande porcentagem do total de linhas, a tabela fica menos eficiente. Recrie o índice columnstore para reduzir o tamanho da tabela, reduzindo a E/S de disco necessária para ler a tabela. Para recriar o índice columnstore, use a opção **Rebuild** da instrução **ALTER INDEX** .  
  
 O columnstore atualizável primeiro insere novos dados em um rowgroup **aberto** , que está no formato de repositório de colunas e, às vezes, é referido como uma tabela Delta.  Quando um rowgroup aberto estiver cheio, seu estado será alterado para **fechado**. Um rowgroup fechado é compactado no formato columnstore pelo motor de tupla e o estado muda para **compactado**.  O Tuple Mover é um processo em segundo plano que periodicamente é acionado e verifica se há algum rowgroup fechado que já esteja pronto para compactar em um rowgroup columnstore.  O Tuple Mover também desaloca todos os rowgroups nos quais cada linha foi excluída. Os RowGroups desalocados são marcados como **marcas de exclusão**. Para executar o movimentador de tupla imediatamente, use a opção **reorganizar** da instrução **ALTER INDEX** .  
  
 Quando um grupo de linhas de columnstore tiver sido preenchido, ele é compactado e para de aceitar novas linhas. Quando as linhas são excluídas de um grupo compactado, elas permanecem, mas são marcadas como excluídas. As atualizações para um grupo compactado são implementadas como uma exclusão do grupo compactado, e uma inserção em um grupo aberto.  
  
## <a name="permissions"></a>Permissões  
 Retorna informações para uma tabela se o usuário tiver a permissão **View definition** na tabela.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir une a tabela **Sys. column_store_row_groups** a outras tabelas do sistema para retornar informações sobre tabelas específicas. A coluna calculada `PercentFull` é uma estimativa da eficiência do grupo de linhas. Para localizar informações em uma única tabela, remova os hifens de comentário na frente da cláusula **Where** e forneça um nome de tabela.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys. column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

