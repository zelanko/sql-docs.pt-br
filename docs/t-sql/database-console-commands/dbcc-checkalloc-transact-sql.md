---
title: DBCC CHECKALLOC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 4cecbb77add5a9afbde3f69bf17ac2bd11bd592b
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Verifica a consistência de estruturas de alocação de espaço em disco para um banco de dados especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_Name* | *database_id* | 0   
 O nome ou a ID do banco de dados para o qual verificar o uso de alocação e página.
Se não for especificado ou se 0 for especificado, o banco de dados atual será usado.
Nomes de banco de dados devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).

 NOINDEX  
 Especifica que os índices não clusterizados para tabelas de usuário não devem ser verificados.<br>NOINDEX é mantido somente para compatibilidade com versões anteriores e não afeta DBCC CHECKALLOC.

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 Especifica que DBCC CHECKALLOC repara os erros encontrados. *Database_Name* deve estar no modo de usuário único.

 REPAIR_ALLOW_DATA_LOSS  
 Tenta reparar qualquer erro encontrado. Esses reparos podem provocar alguma perda de dados. REPAIR_ALLOW_DATA_LOSS é a única opção que permite que erros de alocação sejam reparados.

 REPAIR_FAST  
 A sintaxe é mantida apenas para compatibilidade com versões anteriores. Nenhuma ação de reparo é executada.

 REPAIR_REBUILD  
 Não aplicável.  
 Use as opções REPAIR apenas como um último recurso. Para reparar erros, recomendamos restaurar de um backup. Operações de reparo não consideram nenhuma das restrições que podem existir em tabelas ou entre tabelas. Se a tabela especificada estiver envolvida em uma ou mais restrições, recomendamos executar DBCC CHECKCONSTRAINTS após uma operação de reparo. Se for necessário usar REPAIR, execute DBCC CHECKDB sem uma opção de reparo para localizar o nível de reparo a ser usado. Se você usar o nível de REPAIR_ALLOW_DATA_LOSS, recomendamos fazer backup do banco de dados antes de executar DBCC CHECKDB com essa opção.

 com  
 Permite que opções sejam especificadas.

 ALL_ERRORMSGS  
 Exibe todas as mensagens de erro. Todas as mensagens de erro são exibidas por padrão. Especificar ou omitir esta opção não têm nenhum efeito.

 NO_INFOMSGS  
 Suprime todas as mensagens informativas e o relatório de espaço utilizado.

 TABLOCK  
 Faz o comando DBCC obter um bloqueio de banco de dados exclusivo.

 ESTIMATE ONLY  
 Exibe a quantidade estimada de espaço em tempdb necessária para executar DBCC CHECKALLOC quando todas as outras opções são especificadas.
  
## <a name="remarks"></a>Comentários  
DBCC CHECKALLOC verifica a alocação de todas as páginas no banco de dados, independentemente do tipo de página ou do tipo de objeto ao qual elas pertencem. Isso também valida as diversas estruturas internas usadas para manter o controle dessas páginas e das relações entre elas.
Se NO_INFOMSGS não for especificado, DBCC CHECKALLOC coletará informações sobre uso de espaço para todos os objetos no banco de dados. Essas informações são impressos junto com os erros encontrados.
  
> [!NOTE]  
>A funcionalidade DBCC CHECKALLOC está incluída no [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md). Isso significa que não é preciso executar DBCC CHECKALLOC separadamente dessas instruções.   DBCC CHECKALLOC não verifica dados FILESTREAM. FILESTREAM armazena BLOBS (objetos binários grandes) no sistema de arquivos.  
  
## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno  
DBCC CHECKALLOC usa um instantâneo de banco de dados interno para fornecer a consistência transacional necessária ao executar essas verificações. Se não for possível criar um instantâneo ou se TABLOCK for especificado, DBCC CHECKALLOC tentará adquirir um bloqueio exclusivo (X) no banco de dados para obter a consistência necessária.
  
> [!NOTE]  
> A execução de DBCC CHECKALLOC em relação a tempdb não executa nenhuma verificação. Isso porque, por razões de desempenho, instantâneos do banco de dados não estão disponíveis em tempdb. Isso significa que não é possível obter a consistência transacional exigida. Parar e iniciar o serviço MSSQLSERVER para resolver quaisquer problemas de alocação de tempdb. Essa ação descarta e recria o banco de dados tempdb.  
  
## <a name="understanding-dbcc-error-messages"></a>Compreendendo mensagens de erro DBCC  
Depois que o comando DBCC CHECKALLOC é encerrado, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará uma conclusão bem-sucedida e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação devido a um erro, a mensagem indica que o comando foi finalizado, um valor de estado e a quantidade de tempo de execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
  
|Estado|Description|  
|---|---|  
|0|O número do erro 8930 foi gerado. Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|  
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|  
|3|Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|4|Uma declaração ou violação de acesso foi detectada.|  
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|  
  
## <a name="error-reporting"></a>Relatório de Erros  
Um arquivo de minidespejo (SQLDUMP*nnnn*. txt) é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório de LOG sempre que DBCC CHECKALLOC detecta um erro de dano. Quando os recursos de coleta de dados Uso de Recursos e Relatório de Erros são habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo é encaminhado automaticamente à [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Os dados coletados são usados para aprimorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
O arquivo de despejo contém os resultados do comando DBCC CHECKALLOC e saídas de diagnóstico adicionais. O arquivo tem DACLs (listas de controle de acesso discricionário) restritas. O acesso é limitado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] membros da função sysadmin e conta de serviço. Por padrão, a função de sysadmin contém todos os membros do grupo BUILTIN\Administradores do Windows e o grupo de administradores locais. O comando DBCC não falhará se o processo de coleta de dados falhar.
  
## <a name="resolving-errors"></a>Resolvendo erros  
Se qualquer erro for relatado pelo DBCC CHECKALLOC, é recomendável restaurar o banco de dados do backup em vez de executar um reparo. Se não existir um backup, executar um reparo pode corrigir os erros relatados, entretanto, a correção dos erros pode exigir que algumas páginas e, portanto, dados sejam excluídos.
Um reparo pode ser executado em uma transação de usuário. Isso permite que alterações sejam revertidas. Se as alterações forem revertidas, o banco de dados ainda conterá erros e deverá ser restaurado de um backup. Depois que os reparos forem concluídos, faça backup do banco de dados.
  
## <a name="result-sets"></a>Conjuntos de resultados  
As tabelas a seguir descrevem as informações retornadas por DBCC CHECKALLOC.
  
|Item|Description|  
|---|---|  
|FirstIAM|Somente para uso interno.|  
|Root|Somente para uso interno.|  
|Dpages|Contagem de páginas de dados.|  
|Pages used|Páginas alocadas.|  
|Dedicated extents|Extensões alocadas ao objeto.<br /><br /> Se forem usadas páginas de alocação mistas, pode haver páginas alocadas sem extensões.|  
  
DBCC CHECKALLOC também relata um resumo de alocação para cada índice e partição em cada arquivo. Esse resumo descreve a distribuição dos dados.
  
|Item|Description|  
|---|---|  
|Reserved pages|As páginas alocadas para o índice e as páginas não usadas em extensões alocadas.|  
|Used pages|Páginas alocadas e usadas pelo índice.|  
|Partition ID|Somente para uso interno.|  
|Alloc unit ID|Somente para uso interno.|  
|Dados em linha|As páginas contêm dados de índice ou de heap.|  
|Dados LOB|As páginas contêm **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **texto**, **ntext**, **xml**, e **imagem** dados.|  
|Dados do estouro de linha|As páginas contêm dados de coluna do comprimento de variável que foram enviados por push para fora da linha.|  
  
DBCC CHECKALLOC retorna o conjunto de resultados a seguir (os valores podem variar), exceto quando ESTIMATEONLY ou NO_INFOMSGS é especificado.
  
```sql
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Quando ESTIMATEONLY é especificado, DBCC CHECKALLOC retorna o conjunto de resultados a seguir.
  
```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Requer associação na função de servidor fixa sysadmin ou da função de banco de dados fixa db_owner.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir executa `DBCC CHECKALLOC` para o banco de dados atual e o banco de dados `AdventureWorks2012`.
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  


