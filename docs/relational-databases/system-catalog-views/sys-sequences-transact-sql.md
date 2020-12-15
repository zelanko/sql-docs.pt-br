---
description: sys.sequences (Transact-SQL)
title: sys. sequences (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51123619f1369b61bcbcba4db8314989cd9a0fd4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472957"
---
# <a name="syssequences-transact-sql"></a>sys.sequences (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contém uma linha para objeto de sequência em um banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||Herda todas as colunas de [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**start_value**|**sql_variant não nulo**|O valor inicial do objeto de sequência. Se o objeto de sequência for reiniciado com ALTER SEQUENCE, ele será reiniciado nesse valor. Quando o objeto de sequência circula, ele prossegue para o **minimum_value** ou **maximum_value**, não para o **start_value**.|  
|**increment**|**sql_variant não nulo**|O valor usado para incrementar o objeto de sequência depois de cada valor gerado.|  
|**minimum_value**|**sql_variant nulo**|O valor mínimo que pode ser gerado pelo objeto de sequência. Depois que esse valor for atingido, o objeto de sequência retornará um erro ao tentar gerar mais valores ou reinicializar, se a opção CYCLE tiver sido especificada. Se nenhum MINVALUE tiver sido especificado, essa coluna retornará o valor mínimo com suporte pelo tipo de dados do gerador de sequência.|  
|**maximum_value**|**sql_variant nulo**|O valor máximo que pode ser gerado pelo objeto de sequência. Depois que esse valor for atingido, o objeto de sequência começará a retornar um erro ao tentar gerar mais valores ou reinicializar, se a opção CYCLE tiver sido especificada. Se nenhum MAXVALUE foi especificado, essa coluna retornará o valor máximo que tem suporte do tipo de dados do objeto de sequência.|  
|**is_cycling**|**bit não nulo**|Retornará 0 se Nenhum CYCLE foi especificado para o objeto de sequência, e 1, se CYCLE tiver sido especificado.|  
|**is_cached**|**bit não nulo**|Retornará 0 se NO CACHE foi especificado para o objeto de sequência, e 1, se CACHE tiver sido especificado.|  
|**cache_size**|**int NULL**|Retorna o tamanho do cache especificado para o objeto de sequência. Essa coluna conterá NULL se a sequência tiver sido criada com a opção NO CACHE ou se CACHE tiver sido especificado sem especificar um tamanho de cache. Se o valor especificado pelo tamanho de cache for maior que o número máximo de valores que podem ser retornados pelo objeto de sequência, esse tamanho de cache que não pode ser obtido ainda será exibido.|  
|**system_type_id**|**tinyint não nulo**|ID do tipo de sistema para o tipo de dados do objeto de sequência.|  
|**user_type_id**|**int NOT NULL**|ID do tipo de dados do objeto de sequência conforme definido pelo usuário.|  
|**precisão**|**tinyint não nulo**|A precisão máxima do tipo de dados.|  
|**scale**|**tinyint não nulo**|A escala máxima do tipo de dados. A escala é retornada junto com a precisão para dar metadados completos aos usuários. A escala é sempre 0 para objetos de sequência porque apenas tipos inteiros são permitidos.|  
|**current_value**|**sql_variant não nulo**|O último valor forçado. Ou seja, o valor retornado da execução mais recente da função NEXT VALUE FOR ou o último valor da execução do procedimento de **sp_sequence_get_range** . Retornará o valor de START WITH se a sequência nunca tiver sido usada.|  
|**is_exhausted**|**bit não nulo**|0 indica que mais valores podem ser gerados a partir da sequência. 1 indica que o objeto de sequência atingiu o parâmetro MAXVALUE e a sequência não está definida como CYCLE. A função NEXT VALUE FOR retornará um erro até que a sequência seja reiniciada com ALTER SEQUENCE.|  
|**last_used_value**|**sql_variant nulo**|Retorna o último valor gerado pela função [Next value for](../../t-sql/functions/next-value-for-transact-sql.md) . Aplica-se ao SQL Server 2017 e posterior.|  
  
## <a name="permissions"></a>Permissões  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, a visibilidade dos metadados em exibições do catálogo é limitada a protegíveis que um usuário possui ou para os quais recebeu alguma permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Sequence Numbers](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
