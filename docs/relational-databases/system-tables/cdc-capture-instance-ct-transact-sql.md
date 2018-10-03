---
title: CDC. &lt;capture_instance&gt;CT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b13f890063246c1557d11a504ccf229bb162057
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621024"
---
# <a name="cdcltcaptureinstancegtct-transact-sql"></a>CDC. &lt;capture_instance&gt;CT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  É a tabela de alteração criada quando os dados de alteração capturados são habilitados uma tabela de origem. A tabela retorna uma linha para cada operação de inserção e exclusão executada contra a tabela de origem, e duas linhas para cada operação de atualização executada contra a tabela de origem. Quando o nome da tabela de alteração não for especificado no momento em que a tabela de origem for habilitada, o nome será derivado. O formato do nome é cdc. *capture_instance*CT onde *capture_instance* é o nome do esquema da tabela de origem e o nome da tabela de origem no formato *schema_table*. Por exemplo, se a tabela **Person. address** na **AdventureWorks** banco de dados de exemplo está habilitado para change data capture, o nome da tabela de alteração derivado seria **cdc. Person_Address_CT**.  
  
 É recomendável que você **não consultar diretamente as tabelas do sistema**. Em vez disso, execute as [CDC. fn_cdc_get_all_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [CDC. fn_cdc_get_net_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) funções.  
  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|LSN (número de sequência de log) associado à transação de confirmação da alteração.<br /><br /> Todas as alterações confirmadas na mesma transação compartilham o mesmo LSN de confirmação. Por exemplo, se uma operação de exclusão na tabela de origem remover duas linhas, a tabela de alteração conterá duas linhas, cada um com o mesmo **_ $start_lsn** valor.|  
|**_ $end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta coluna é sempre NULL.|  
|**__$seqval**|**binary(10)**|Valor de sequência usado para ordenar as alterações de linha em uma transação.|  
|**__$operation**|**int**|Identifica a operação DML (linguagem de manipulação de dados) associada com a alteração. Pode ser uma destas opções:<br /><br /> 1 = excluir<br /><br /> 2 = inserir<br /><br /> 3 = atualizar (valores antigos)<br /><br /> Os dados de coluna têm valores de linha antes de executar a instrução de atualização.<br /><br /> 4 = atualizar (valores novos)<br /><br /> Os dados de coluna têm valores de linha depois de executar a instrução de atualização.|  
|**__$update_mask**|**varbinary(128)**|Uma máscara de bits com base nos ordinais de coluna da tabela de alteração que identificam as colunas que foram alteradas.|  
|*\<colunas da tabela de origem capturada>*|varia|As colunas restantes na tabela de alteração são as colunas da tabela de origem que foram identificadas como colunas capturadas quando a instância de captura foi criada. Se nenhuma coluna tiver sido especificada na lista de colunas capturadas, todas as colunas da tabela de origem serão incluídas nessa tabela.|  
|**_ $command_id** |**int** |Controla a ordem das operações em uma transação. |  
  
## <a name="remarks"></a>Comentários  

O `__$command_id` coluna foi a coluna foi introduzida em uma atualização cumulativa em versões de 2012 até 2016. Para obter informações de versão e o download, consulte o artigo KB 3030352 em [corrigir: A tabela de alteração é ordenada incorretamente para atualizada linhas depois de habilitar dados de alteração de captura para um banco de dados do Microsoft SQL Server](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you).  Para obter mais informações, consulte [funcionalidade de CDC pode falhar após a atualização para o CU mais recente do SQL Server 2012, 2014 e 2016](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/).

## <a name="captured-column-data-types"></a>Tipos de dados da coluna capturada  
 As colunas capturadas incluídas nesta tabela têm o mesmo tipo de dados e valor que suas colunas de origem correspondentes com as exceções a seguir:  
  
-   **Carimbo de hora** as colunas são definidas como **binary (8)**.  
  
-   **Identidade** colunas são definidas como **int** ou **bigint**.  
  
 No entanto, os valores nessas colunas são iguais aos valores da coluna de origem.  
  
### <a name="large-object-data-types"></a>Tipos de dados de objeto grande  
 Colunas de tipo de dados **imagem**, **texto**, e **ntext** sempre são atribuídos um **nulo** valor quando _ $operation = 1 ou \_ \_$operation = 3. Colunas de tipo de dados **varbinary (max)**, **varchar (max)**, ou **nvarchar (max)** recebem um **nulo** valor quando \_ \_$operation = 3, a menos que a coluna alterada durante a atualização. Quando \_ \_$operation = 1, essas colunas são atribuídas a seu valor no momento da exclusão. Colunas computadas que são incluídas em uma instância de captura sempre têm um valor de **nulo**.  
  
 Por padrão, o tamanho máximo que pode ser adicionado a uma coluna capturada em uma única instrução INSERT, UPDATE, WRITETEXT ou UPDATETEXT é de 65.536 bytes ou 64 KB. Para aumentar esse tamanho para dar suporte a dados LOB maiores, use o [configurar a opção de configuração do servidor do max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) para especificar um tamanho máximo maior. Para obter mais informações, veja [Configurar a opção max text repl size de configuração de servidor](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md).  
  
## <a name="data-definition-language-modifications"></a>Modificações da linguagem de definição de dados  
 As modificações de DDL da tabela de origem, como adicionar ou descartar colunas, são registradas na [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) tabela. Essas alterações não serão aplicadas à tabela de alterações. Ou seja, a definição da tabela de alteração permanece constante. Ao inserir linhas na tabela de alteração, o processo de captura ignora as colunas que não aparecem na lista de colunas capturadas associadas à tabela de origem. Se uma coluna aparecer na lista de colunas capturadas e não estiver mais na tabela de origem, será atribuído um valor nulo à coluna.  
  
 Alterar o tipo de dados de uma coluna na tabela de origem também é registrada na [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) tabela. No entanto, essa alteração modifica a definição da tabela de alteração. Os tipos de dados da coluna capturada na tabela de alteração são modificados quando o processo de captura encontrar o registro de log para a alteração de DDL feita na tabela de origem.  
  
 Se você precisar modificar o tipo de dados de uma coluna capturada na tabela de origem de forma a diminuir o tamanho do tipo de dados, use o procedimento a seguir para assegurar que a coluna equivalente na tabela de alteração poderá ser modificada com êxito.  
  
1.  Na tabela de origem, atualize os valores na coluna a ser modificada para que se ajustem ao tamanho do tipo de dados planejado. Por exemplo, se você alterar o tipo de dados do **int** para **smallint**, atualize os valores para um tamanho que se ajusta a **smallint** intervalo de -32.768 a 32.767.  
  
2.  Na tabela de alteração, execute a mesma operação de atualização na coluna equivalente.  
  
3.  Altere a tabela de origem especificando o novo tipo de dados. A alteração do tipo de dados é propagada com êxito na tabela de alteração.  
  
## <a name="data-manipulation-language-modifications"></a>Modificações da linguagem de manipulação de dados  
 Quando as operações de inserção, atualização e exclusão forem executadas em uma tabela de origem com a captura de dados de alteração habilitada, um registro dessas operações DML aparecerão no log de transações do banco de dados. O processo de captura de dados de alteração recupera informações sobre alterações do log de transações e insere uma ou duas linhas na tabela de alteração para registrar a alteração. As entradas são adicionadas à tabela de alteração na mesma ordem em que foram confirmadas na tabela de origem, embora a confirmação das entradas da tabela de alterações normalmente deva ser feita em um grupo de alterações e não para uma única entrada.  
  
 Dentro da entrada de tabela de alteração, o **_ $start_lsn** coluna é usada para registrar o LSN que está associado com a alteração para a tabela de origem de confirmação e o **coluna do _ $seqval** é usada para ordenar a alteração em sua transação. Juntas, essas colunas de metadados podem ser usadas para garantir que a ordem de confirmação das  alterações de origem será preservada. Como o processo de captura obtém as informações sobre alterações do log de transações, é importante observar que as entradas da tabela de alteração não aparecem de forma sincronizada com as alterações da tabela de origem correspondente. Em vez disso, as alterações correspondentes aparecem de forma assíncrona, depois que o processo de captura processou as entradas de alteração pertinentes do log de transação.  
  
 Para as operações de inserção e exclusão, todos os bits na máscara de atualização estão definidos. Para operações de atualização, a máscara de atualização nas linhas da antiga atualização e da nova atualização será modificada para refletir as colunas alteradas durante a atualização.  
  
## <a name="see-also"></a>Consulte também  
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
