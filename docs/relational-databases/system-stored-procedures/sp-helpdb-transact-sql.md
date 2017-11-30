---
title: sp_helpdb (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 46eb86009bf940857788425afd4781ca79ab3686
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre um banco de dados especificado ou todos os bancos de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=** ] **'***nome***'**  
 É o nome do banco de dados cujas informações são reportadas. *nome* é **sysname**, sem padrão. Se *nome* não for especificado, **sp_helpdb** relatórios em todos os bancos de dados de **sys. Databases** exibição do catálogo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados.|  
|**db_size**|**nvarchar(13)**|Tamanho total do banco de dados.|  
|**proprietário**|**sysname**|Proprietário do banco de dados como **sa**.|  
|**DBID**|**smallint**|ID do banco de dados.|  
|**criado**|**nvarchar(11)**|A data em que o banco de dados foi criado.|  
|**status**|**nvarchar(600)**|Lista de valores separados por vírgula de opções de banco de dados que estão atualmente definidas no banco de dados.<br /><br /> As opções avaliadas como boolianas serão listadas apenas se estiverem habilitadas. Opções não Boolianas são listadas com seus valores correspondentes na forma de *option_name*=*valor*.<br /><br /> Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**compatibility_level**|**tinyint**|Nível de compatibilidade do banco de dados: 60, 65, 70, 80 ou 90.|  
  
 Se *nome* for especificado, há um conjunto de resultados adicionais que mostra a alocação de arquivo para o banco de dados especificado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|Nome do arquivo lógico.|  
|**FileID**|**smallint**|ID do arquivo.|  
|**nome de arquivo**|**nchar(260)**|Nome do arquivo do -sistema operacional (nome do arquivo físico).|  
|**grupo de arquivos**|**nvarchar (128)**|Grupo de arquivos ao qual o arquivo pertence.<br /><br /> NULL = ele é um arquivo de log. Ele nunca faz parte de um grupo de arquivos.|  
|**tamanho**|**nvarchar(18)**|Tamanho do arquivo em megabytes.|  
|**MaxSize**|**nvarchar(18)**|Tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**crescimento**|**nvarchar(18)**|Incremento de crescimento do arquivo. Indica a quantidade de espaço adicionada ao arquivo sempre que um novo espaço for necessário.|  
|**uso**|**varchar (9)**|Uso do arquivo Para um arquivo de dados, o valor é **'dados'** e para o arquivo de log é o valor **'log apenas'**.|  
  
## <a name="remarks"></a>Comentários  
 O **status** relatórios quais opções foram definidas como ON no banco de dados do conjunto de colunas no resultado. Todas as opções de banco de dados não são relatadas pelo **status** coluna. Para ver uma lista completa das configurações de opção de banco de dados atual, use o **sys. Databases** exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Quando um banco de dados for especificado, associação a **pública** função no banco de dados é necessária. Quando nenhum banco de dados é especificado, associação a **pública** função no **mestre** banco de dados é necessário.  
  
 Se um banco de dados não pode ser acessado, **sp_helpdb** exibe informações de 15622 e o máximo de mensagem de erro sobre o banco de dados possível.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-a-single-database"></a>A. Retornando informações sobre um único banco de dados  
 O exemplo a seguir exibe informações sobre o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```tsql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. Retornando informações sobre todos os bancos de dados  
 O exemplo a seguir exibe informações sobre todos os bancos de dados no servidor que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```tsql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys. filegroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
