---
title: core.sp_purge_data (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cbcd8616fc743ee749b3adb9b30f343939fa7f3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819234"
---
# <a name="coresppurgedata-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove dados do data warehouse de gerenciamento com base em uma política de retenção. Esse procedimento é executado diariamente pelo mdw_purge_data[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente no data warehouse de gerenciamento associado à instância especificada. Você pode usar esse procedimento armazenado para executar uma remoção sob demanda de dados do data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@retention_days =] *retention_days*  
 O número de dias para reter dados nas tabelas do data warehouse de gerenciamento. Dados com um carimbo de hora anterior a *retention_days* é removido. *retention_days* está **smallint**, com um padrão NULL. Se especificado, o valor deverá ser positivo. Quando NULL, o valor na coluna valid_through no modo de exibição snapshots determina as linhas que estão qualificadas para remoção.  
  
 [@instance_name =] '*instance_name*'  
 O nome da instância do conjunto de coleta. *nome_da_instância* está **sysname**, com um padrão NULL.  
  
 *nome_da_instância* deve ser o nome totalmente qualificado da instância, que consiste o nome do computador e o nome da instância no formato *computername*\\*instancename*. Quando NULL, a instância padrão no servidor local será usada.  
  
 [@collection_set_uid =] '*collection_set_uid*'  
 O GUID do conjunto de coleta. *collection_set_uid* está **uniqueidentifier**, com um padrão NULL. Quando NULL, as linhas de qualificação de todos os conjuntos de coleta serão removidas. Para obter esse valor, consulte a exibição do catálogo syscollector_collection_sets.  
  
 [@duration =] *duração*  
 O número máximo de minutos em que a operação de limpeza deve ser executada. *duração* está **smallint**, com um padrão NULL. Se especificado, o valor deve ser zero ou um inteiro positivo. Quando NULL, a operação será executada até que todas as linhas qualificadas sejam removidas ou que a operação seja interrompida manualmente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Este procedimento seleciona linhas na exibição core.snapshots que se qualificam para remoção com base em um período de retenção. Todas as linhas qualificadas para remoção são excluídas da tabela core.snapshots_internal. A exclusão das linhas precedentes dispara a ação de exclusão em cascata em todas as tabelas do data warehouse de gerenciamento. Isso é feito por meio da cláusula ON DELETE CASCADE definida para todas as tabelas que armazenam dados coletados.  
  
 Cada instantâneo e seus dados associados são excluídos dentro de uma transação explícita e confirmados. Portanto, se a operação de limpeza for interrompida manualmente ou se o valor especificado para @duration for excedido, o dados não confirmados permanecerão. Esses dados podem ser removidos na próxima execução do trabalho.  
  
 O procedimento deve ser executado no contexto do banco de dados do data warehouse de gerenciamento.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **mdw_admin** (com permissão EXECUTE) a função de banco de dados fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-sppurgedata-with-no-parameters"></a>A. Executando sp_purge_data sem nenhum parâmetro  
 O exemplo a seguir executa core.sp_purge_data sem especificar nenhum parâmetro. Portanto, o valor padrão de NULL é usado para todos os parâmetros com o comportamento associado.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. Especificando valores de retenção e duração  
 O exemplo a seguir remove os dados com mais de sete dias do data warehouse de gerenciamento. Além disso, o @duration parâmetro for especificado, para que a operação seja executada mais do que 5 minutos.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. Especificando um nome de instância e um conjunto de coleta  
 O exemplo a seguir remove os dados do data warehouse de gerenciamento para um determinado conjunto de coleta na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porque @retention_days não for especificado, o valor na coluna valid_through no modo de exibição snapshots é usado para determinar as linhas no conjunto de coleta que estão qualificadas para remoção.  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
