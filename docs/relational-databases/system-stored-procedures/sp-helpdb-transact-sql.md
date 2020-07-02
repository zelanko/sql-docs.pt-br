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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3a31eb5fa85ab7634d6fc65ac446607117ec70ad
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738518"
---
# <a name="sp_helpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Relata informações sobre um banco de dados especificado ou todos os bancos de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'name'`É o nome do banco de dados para o qual as informações são relatadas. o *nome* é **sysname**, sem padrão. Se o *nome* não for especificado, **sp_helpdb** relatórios em todos os bancos de dados na exibição de catálogo **Sys. databases** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|nome do banco de dados.|  
|**db_size**|**nvarchar (13)**|Tamanho total do banco de dados.|  
|**proprietário**|**sysname**|Proprietário do banco de dados, como **SA**.|  
|**DBID**|**smallint**|ID do banco de dados.|  
|**created**|**nvarchar(11)**|A data em que o banco de dados foi criado.|  
|**status**|**nvarchar (600)**|Lista de valores separados por vírgula de opções de banco de dados que estão atualmente definidas no banco de dados.<br /><br /> As opções avaliadas como boolianas serão listadas apenas se estiverem habilitadas. As opções não booleanas são listadas com seus valores correspondentes na forma de *option_name* = *valor*.<br /><br /> Para obter mais informações, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**compatibility_level**|**tinyint**|Nível de compatibilidade do banco de dados: 60, 65, 70, 80 ou 90.|  
  
 Se *Name* for especificado, haverá um conjunto de resultados adicional que mostra a alocação de arquivo para o banco de dados especificado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|Nome do arquivo lógico.|  
|**FileID**|**smallint**|ID do arquivo.|  
|**nome do arquivo**|**nchar (260)**|Nome do arquivo do -sistema operacional (nome do arquivo físico).|  
|**grupo de arquivos**|**nvarchar(128)**|Grupo de arquivos ao qual o arquivo pertence.<br /><br /> NULL = ele é um arquivo de log. Ele nunca faz parte de um grupo de arquivos.|  
|**size**|**nvarchar (18)**|Tamanho do arquivo em megabytes.|  
|**MaxSize**|**nvarchar (18)**|Tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**growth**|**nvarchar (18)**|Incremento de crescimento do arquivo. Indica a quantidade de espaço adicionada ao arquivo sempre que um novo espaço for necessário.|  
|**usos**|**varchar (9)**|Uso do arquivo Para um arquivo de dados, o valor é **' somente dados '** e, para o arquivo de log, o valor é **' log only '**.|  
  
## <a name="remarks"></a>Comentários  
 A coluna **status** no conjunto de resultados informa quais opções foram definidas como on no banco de dados. Todas as opções de banco de dados não são relatadas pela coluna **status** . Para ver uma lista completa das configurações de opção de banco de dados atual, use a exibição de catálogo **Sys. databases** .  
  
## <a name="permissions"></a>Permissões  
 Quando um único banco de dados é especificado, a associação na função **pública** no banco de dados é necessária. Quando nenhum banco de dados é especificado, a associação na função **pública** no banco de dados **mestre** é necessária.  
  
 Se um banco de dados não puder ser acessado, **sp_helpdb** exibirá a mensagem de erro 15622 e o máximo possível de informações sobre o banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-a-single-database"></a>a. Retornando informações sobre um único banco de dados  
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
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [os grupos de sys. File&#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
