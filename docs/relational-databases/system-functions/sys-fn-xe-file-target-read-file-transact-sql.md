---
title: sys. fn_xe_file_target_read_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b4ee24b0ee74540a967c713579365c68aa849dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738568"
---
# <a name="sysfn_xe_file_target_read_file-transact-sql"></a>sys.fn_xe_file_target_read_file (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Lê arquivos que são criados pelo destino de arquivos assíncronos do mecanismo de Eventos estendidos. É retornado um evento, em formato XML, por linha.  
  
> [!WARNING]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] aceite os resultados de rastreamento gerados no formato Xel e XEM. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Os eventos estendidos dão suporte apenas a resultados de rastreamento no formato XEL. É recomendável usar o SQL Server Management Studio para ler resultados de rastreamento no formato XEL.    
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_xe_file_target_read_file ( path, mdpath, initial_file_name, initial_offset )  
```  
  
## <a name="arguments"></a>Argumentos  
 *path*  
 O caminho para os arquivos a serem lidos. o *caminho* pode conter curingas e incluir o nome de um arquivo. o *caminho* é **nvarchar (260)**. Não há nenhum padrão. No contexto do banco de dados SQL do Azure, esse valor é uma URL HTTP para um arquivo no armazenamento do Azure.
  
 *mdpath*  
 O caminho para o arquivo de metadados que corresponde ao arquivo ou aos arquivos especificados pelo argumento *path* . *mdpath* é **nvarchar (260)**. Não há nenhum padrão. A partir do SQL Server 2016, esse parâmetro pode ser fornecido como nulo.
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Não requer o parâmetro *mdpath* . No entanto, é mantido para compatibilidade com versões anteriores para arquivos de log gerados nas versões anteriores do SQL Server.  
  
 *initial_file_name*  
 O primeiro arquivo a ser lido a partir do *caminho*. *initial_file_name* é **nvarchar (260)**. Não há nenhum padrão. Se **NULL** for especificado como o argumento, todos os arquivos encontrados no *caminho* serão lidos.  
  
> [!NOTE]  
>  *initial_file_name* e *initial_offset* são argumentos emparelhados. Se você especificar um valor um dos argumentos, deverá especificar um valor para o outro argumento.  
  
 *initial_offset*  
 Usado para especificar o último deslocamento lido anteriormente e o ignora todos os eventos até o deslocamento (inclusive). A enumeração de evento é iniciada após o deslocamento especificado. *initial_offset* é **bigint**. Se **NULL** for especificado como o argumento, o arquivo inteiro será lido.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|module_guid|**uniqueidentifier**|O módulo de evento GUID. Não permite valor nulo.|  
|package_guid|**uniqueidentifier**|O pacote de evento GUID. Não permite valor nulo.|  
|object_name|**nvarchar(256)**|O nome do evento. Não permite valor nulo.|  
|event_data|**nvarchar(max)**|Os conteúdos de evento no formato XML. Não permite valor nulo.|  
|file_name|**nvarchar(260)**|O nome do arquivo que contém o evento. Não permite valor nulo.|  
|file_offset|**bigint**|O deslocamento do bloco no arquivo que contém o evento. Não permite valor nulo.|  
|timestamp_utc|**datetime2**|**Aplica-se a**: [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br />A data e hora (fuso horário UTC) do evento. Não permite valor nulo.|  

  
## <a name="remarks"></a>Comentários  
 Ler grandes conjuntos de resultados executando **Sys. fn_xe_file_target_read_file** em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] pode resultar em um erro. Use os **resultados para** o modo de arquivo (**Ctrl + Shift + F**) para exportar grandes conjuntos de resultados para um arquivo e ler o arquivo com outra ferramenta em vez disso.  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-data-from-file-targets"></a>a. Recuperando dados de destinos de arquivo  
 O exemplo a seguir usa todas as linhas de todos os arquivos. Neste exemplo, os destinos de arquivo e metarquivos estão localizados na pasta de rastreamento na unidade C: \.  
  
```  
SELECT * FROM sys.fn_xe_file_target_read_file('C:\traces\*.xel', 'C:\traces\metafile.xem', null, null);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Exibições de catálogo de eventos estendidos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
