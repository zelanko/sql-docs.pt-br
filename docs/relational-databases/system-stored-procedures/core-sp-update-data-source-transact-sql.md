---
title: sp_update_data_source (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8bdbab374f7f6fa182ea344f442b23e2dec2a15b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766465"
---
# <a name="corespupdatedatasource-transact-sql"></a>core.sp_update_data_source (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza uma linha existente ou insere uma nova linha na tabela core.source_info_internal do data warehouse de gerenciamento. Esse procedimento é chamado pelo componente de tempo de execução do coletor de dados sempre que um pacote de carregamento começa a carregar dados no data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_uid =] '*collection_set_uid*'  
 O GUID do conjunto de coleta. *collection_set_uid* está **uniqueidentifier**, sem nenhum valor padrão. Para obter o GUID, consulte a exibição dbo.syscollector_collection_sets no banco de dados msdb.  
  
 [ @machine_name =] '*machine_name*'  
 O nome do servidor no qual o conjunto de coleta reside. *nome_do_computador* está **sysname** sem nenhum valor padrão.  
  
 [ @named_instance =] '*instância_nomeada*'  
 O nome da instância do conjunto de coleta. *instância_nomeada* está **sysname**, sem nenhum valor padrão.  
  
> [!NOTE]  
>  *instância_nomeada* deve ser o nome totalmente qualificado da instância, que consiste o nome do computador e o nome da instância no formato *computername*\\*instancename*.  
  
 [ @days_until_expiration =] *days_until_expiration*  
 O número de dias restantes no período de retenção de dados do instantâneo. *days_until_expiration* está **smallint**.  
  
 [ @source_id =] *source_id*  
 O identificador exclusivo da origem da atualização. *source_id* está **int** e é retornada como OUTPUT.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Toda vez que um pacote de carregamento inicia o carregamento de dados no data warehouse de gerenciamento, o componente de tempo de execução do coletor de dados chama core.sp_update_data_source. A tabela core.source_info_internal será atualizada se uma das seguintes alterações tiver ocorrido desde o último carregamento:  
  
-   Um novo conjunto de coleta foi adicionado.  
  
-   O valor de days_until_expiration foi alterado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **mdw_writer** (com permissão EXECUTE) a função de banco de dados fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza a fonte de dados (nesse caso, o conjunto de coleta Uso do Disco), define o número de dias até a expiração e retorna o identificador da fonte. No exemplo, a instância padrão é usada.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Data warehouse de gerenciamento](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
