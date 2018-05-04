---
title: sys. fn_xe_file_target_read_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_xe_file_target_read_file_TSQL
- fn_xe_file_target_read_file
- sys.fn_xe_file_target_read_file_TSQL
- sys.fn_xe_file_target_read_file
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], functions
- fn_xe_file_target_read_file function
- sys.fn_xe_file_target_read_file function
ms.assetid: cc0351ae-4882-4b67-b0d8-bd235d20c901
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb58db9e3e74ad34e01faa4fbb2520813dc135b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnxefiletargetreadfile-transact-sql"></a>sys.fn_xe_file_target_read_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Lê arquivos que são criados pelo destino de arquivos assíncronos do mecanismo de Eventos estendidos. É retornado um evento, em formato XML, por linha.  
  
> [!WARNING]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] aceitam resultados de rastreamento gerados no formato XEL e XEM. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Suporte estendido de eventos somente resultados de rastreamento no formato XEL. É recomendável usar o SQL Server Management Studio para ler resultados de rastreamento no formato XEL.    
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_xe_file_target_read_file ( path, mdpath, initial_file_name, initial_offset )  
```  
  
## <a name="arguments"></a>Argumentos  
 *path*  
 O caminho para os arquivos a serem lidos. *caminho* pode conter curingas e incluir o nome de um arquivo. *caminho* é **nvarchar (260)**. Não há nenhum padrão. No contexto do banco de dados do SQL Azure, esse valor é uma URL de HTTP para um arquivo no armazenamento do Azure.
  
 *mdpath*  
 O caminho para o arquivo de metadados que corresponde ao arquivo ou arquivos especificados pelo *caminho* argumento. *mdpath* é **nvarchar (260)**. Não há nenhum padrão. Começando com o SQL Server 2016, esse parâmetro pode ser fornecido como nulo.
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] não exige o *mdpath* parâmetro. No entanto, é mantido para compatibilidade com versões anteriores para arquivos de log gerados nas versões anteriores do SQL Server.  
  
 *initial_file_name*  
 O primeiro arquivo leiam *caminho*. *initial_file_name* é **nvarchar (260)**. Não há nenhum padrão. Se **nulo** é especificado como argumento de todos os arquivos encontrados na *caminho* são lidos.  
  
> [!NOTE]  
>  *initial_file_name* e *initial_offset* são argumentos emparelhados. Se você especificar um valor um dos argumentos, deverá especificar um valor para o outro argumento.  
  
 *initial_offset*  
 Usado para especificar o último deslocamento lido anteriormente e o ignora todos os eventos até o deslocamento (inclusive). A enumeração de evento é iniciada após o deslocamento especificado. *initial_offset* é **bigint**. Se **nulo** é especificado como o argumento do arquivo inteiro será lido.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|module_guid|**uniqueidentifier**|O módulo de evento GUID. Não permite valor nulo.|  
|package_guid|**uniqueidentifier**|O pacote de evento GUID. Não permite valor nulo.|  
|object_name|**nvarchar(256)**|O nome do evento. Não permite valor nulo.|  
|event_data|**nvarchar(max)**|Os conteúdos de evento no formato XML. Não permite valor nulo.|  
|file_name|**nvarchar(260)**|O nome do arquivo que contém o evento. Não permite valor nulo.|  
|file_offset|**bigint**|O deslocamento do bloco no arquivo que contém o evento. Não permite valor nulo.|  
|timestamp_utc|**datetime2**|**Aplica-se a**: [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br />A data e hora (fuso horário UTC) do evento. Não permite valor nulo.|  

  
## <a name="remarks"></a>Remarks  
 Ler resultados grandes define executando **fn_xe_file_target_read_file** em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] pode resultar em um erro. Use o **resultados em arquivo** modo (**Ctrl + Shift + F**) para exportar grandes conjuntos de resultados para um arquivo e ler o arquivo em outra ferramenta em vez disso.  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-data-from-file-targets"></a>A. Recuperando dados de destinos de arquivo  
 O exemplo a seguir usa todas as linhas de todos os arquivos. Neste exemplo, os destinos de arquivo e metarquivos estão localizados na pasta de rastreamento na unidade C: \.  
  
```  
SELECT * FROM sys.fn_xe_file_target_read_file('C:\traces\*.xel', 'C:\traces\metafile.xem', null, null);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Exibições de catálogo de eventos estendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
