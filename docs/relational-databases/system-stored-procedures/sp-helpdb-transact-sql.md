---
title: sp_helpdb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7acc14d3950e0e2d1004727b2efbffd2e4963a2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903015"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre um banco de dados especificado ou todos os bancos de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'name'` É o nome do banco de dados para os quais informações são relatadas. *nome da* está **sysname**, sem padrão. Se *nome* não for especificado, **sp_helpdb** relatórios em todos os bancos de dados a **sys. Databases** exibição do catálogo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados.|  
|**db_size**|**nvarchar(13)**|Tamanho total do banco de dados.|  
|**owner**|**sysname**|Banco de dados proprietário, como **sa**.|  
|**dbid**|**smallint**|ID do banco de dados.|  
|**created**|**nvarchar(11)**|A data em que o banco de dados foi criado.|  
|**status**|**nvarchar(600)**|Lista de valores separados por vírgula de opções de banco de dados que estão atualmente definidas no banco de dados.<br /><br /> As opções avaliadas como boolianas serão listadas apenas se estiverem habilitadas. Opções não Boolianas são listadas com seus valores correspondentes na forma de *option_name*=*valor*.<br /><br /> Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**compatibility_level**|**tinyint**|Nível de compatibilidade do banco de dados: 60, 65, 70, 80 ou 90.|  
  
 Se *nome* for especificado, há um conjunto de resultados adicionais que mostra a alocação de arquivo para o banco de dados especificado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|Nome do arquivo lógico.|  
|**fileid**|**smallint**|ID do arquivo.|  
|**filename**|**nchar(260)**|Nome do arquivo do -sistema operacional (nome do arquivo físico).|  
|**filegroup**|**nvarchar(128)**|Grupo de arquivos ao qual o arquivo pertence.<br /><br /> NULL = ele é um arquivo de log. Ele nunca faz parte de um grupo de arquivos.|  
|**size**|**nvarchar(18)**|Tamanho do arquivo em megabytes.|  
|**maxsize**|**nvarchar(18)**|Tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**growth**|**nvarchar(18)**|Incremento de crescimento do arquivo. Indica a quantidade de espaço adicionada ao arquivo sempre que um novo espaço for necessário.|  
|**Uso**|**varchar(9)**|Uso do arquivo Para um arquivo de dados, o valor será **'dados'** e para o arquivo de log é o valor **'log apenas'** .|  
  
## <a name="remarks"></a>Comentários  
 O **status** quais opções foram definidas como ON no banco de dados de relatórios do conjunto de colunas no resultado. Todas as opções de banco de dados não são informadas por meio de **status** coluna. Para ver uma lista completa das configurações de opção de banco de dados atual, use o **sys. Databases** exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Quando um banco de dados é especificado, associação à **pública** função no banco de dados é necessária. Quando nenhum banco de dados for especificado, associação a **pública** função no **mestre** banco de dados é necessário.  
  
 Se um banco de dados não pode ser acessado, **sp_helpdb** exibe informações de 15622 e de mensagem de erro sobre o banco de dados quanto possível.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-a-single-database"></a>A. Retornando informações sobre um único banco de dados  
 O exemplo a seguir exibe informações sobre o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. Retornando informações sobre todos os bancos de dados  
 O exemplo a seguir exibe informações sobre todos os bancos de dados no servidor que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
