---
title: Core. sp_purge_data (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 27f2d95a23a89c4e50924944709ba38a39a6ff2d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833659"
---
# <a name="coresp_purge_data-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove dados do data warehouse de gerenciamento com base em uma política de retenção. Este procedimento é executado diariamente pelo trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mdw_purge_data em relação ao data warehouse de gerenciamento associado à instância especificada. Você pode usar esse procedimento armazenado para executar uma remoção sob demanda de dados do data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @retention_days =] *retention_days*  
 O número de dias para reter dados nas tabelas do data warehouse de gerenciamento. Os dados com um carimbo de data/hora mais antigo que *retention_days* são removidos. *retention_days* é **smallint**, com um padrão de NULL. Se especificado, o valor deverá ser positivo. Quando NULL, o valor na coluna valid_through na exibição core. Snapshots determina as linhas qualificadas para remoção.  
  
 [ @instance_name =] '*instance_name*'  
 O nome da instância do conjunto de coleta. *instance_name* é **sysname**, com um padrão de NULL.  
  
 *instance_name* deve ser o nome de instância totalmente qualificado, que consiste no nome do computador e no nome da instância no formato *ComputerName* \\ *InstanceName*. Quando NULL, a instância padrão no servidor local será usada.  
  
 [ @collection_set_uid =] '*collection_set_uid*'  
 O GUID do conjunto de coleta. *collection_set_uid* é **uniqueidentifier**, com um padrão de NULL. Quando NULL, as linhas de qualificação de todos os conjuntos de coleta serão removidas. Para obter esse valor, consulte a exibição do catálogo syscollector_collection_sets.  
  
 [ @duration =] *duração*  
 O número máximo de minutos em que a operação de limpeza deve ser executada. a *duração* é **smallint**, com um padrão de NULL. Se especificado, o valor deve ser zero ou um inteiro positivo. Quando NULL, a operação será executada até que todas as linhas qualificadas sejam removidas ou que a operação seja interrompida manualmente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Este procedimento seleciona linhas na exibição core.snapshots que se qualificam para remoção com base em um período de retenção. Todas as linhas qualificadas para remoção são excluídas da tabela core.snapshots_internal. A exclusão das linhas precedentes dispara a ação de exclusão em cascata em todas as tabelas do data warehouse de gerenciamento. Isso é feito por meio da cláusula ON DELETE CASCADE definida para todas as tabelas que armazenam dados coletados.  
  
 Cada instantâneo e seus dados associados são excluídos dentro de uma transação explícita e confirmados. Portanto, se a operação de limpeza for interrompida manualmente ou se o valor especificado para @duration for excedido, somente os dados não confirmados permanecerão. Esses dados podem ser removidos na próxima execução do trabalho.  
  
 O procedimento deve ser executado no contexto do banco de dados do data warehouse de gerenciamento.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **mdw_admin** (com permissão de execução).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-sp_purge_data-with-no-parameters"></a>a. Executando sp_purge_data sem nenhum parâmetro  
 O exemplo a seguir executa core.sp_purge_data sem especificar nenhum parâmetro. Portanto, o valor padrão de NULL é usado para todos os parâmetros com o comportamento associado.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. Especificando valores de retenção e duração  
 O exemplo a seguir remove os dados com mais de sete dias do data warehouse de gerenciamento. Além disso, o @duration parâmetro é especificado para que a operação seja executada em não mais de 5 minutos.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. Especificando um nome de instância e um conjunto de coleta  
 O exemplo a seguir remove os dados do data warehouse de gerenciamento para um determinado conjunto de coleta na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como @retention_days não é especificado, o valor na coluna valid_through na exibição core. Snapshots é usado para determinar as linhas do conjunto de coleta que são elegíveis para remoção.  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
