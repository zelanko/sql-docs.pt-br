---
title: DBCC CHECKFILEGROUP (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKFILEGROUP_TSQL
- DBCC_CHECKFILEGROUP_TSQL
- DBCC CHECKFILEGROUP
- CHECKFILEGROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKFILEGROUP statement
- database objects [SQL Server], checking
- allocation checks
- integrity [SQL Server], database objects
- filegroups [SQL Server], consistency checks
- table integrity checks [SQL Server]
- checking database objects
ms.assetid: 8c70bf34-7570-4eb6-877a-e35064a1380a
caps.latest.revision: 60
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6e5335bd6685e1c547361d931938134becaac84
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkfilegroup-transact-sql"></a>DBCC CHECKFILEGROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Verifica a alocação e integridade estrutural de todas as tabelas e exibições indexadas no grupo de arquivos especificado do banco de dados atual.
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DBCC CHECKFILEGROUP   
[  
    [ ( { filegroup_name | filegroup_id | 0 }   
        [ , NOINDEX ]   
  ) ]  
    [ WITH   
        {   
            [ ALL_ERRORMSGS | NO_INFOMSGS ]   
            [ , TABLOCK ]   
            [ , ESTIMATEONLY ]  
            [ , PHYSICAL_ONLY ]    
            [ , MAXDOP  = number_of_processors ]  
        }   
    ]  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 *filegroup_name*  
 É o nome do grupo de arquivos no banco de dados atual para o qual a alocação e integridade estrutural de tabela devem ser verificadas. Se não for especificado, ou se 0 for especificado, o padrão será o grupo de arquivos primário. Nomes de grupo de arquivos devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
 *filegroup_name* não pode ser um grupo de arquivos FILESTREAM.  
  
 *filegroup_id*  
 É a ID (número de identificação) do grupo de arquivos no banco de dados atual para o qual a alocação e a integridade estrutural da tabela devem ser verificadas.  
  
 NOINDEX  
 Especifica que não devem ser executadas verificações intensivas de índices não clusterizados de tabelas de usuário. Isto reduz o tempo de execução geral. NOINDEX não afeta tabelas do sistema porque DBCC CHECKFILEGROUP sempre verifica todos os índices de tabela de sistema.  
  
 ALL_ERRORMSGS  
 Exibe um número ilimitado de erros por objeto. Todas as mensagens de erro são exibidas por padrão. Especificar ou omitir esta opção não têm nenhum efeito.  
  
 NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
 TABLOCK  
 Faz com que DBCC CHECKFILEGROUP obtenha bloqueios em vez de usar um instantâneo do banco de dados interno.  
  
 ESTIMATE ONLY  
 Exibe a quantidade estimada de espaço tempdb necessária para executar DBCC CHECKFILEGROUP com todas as outras opções especificadas.  
  
 PHYSICAL_ONLY  
 Limita a verificação à integridade da estrutura física da página, dos cabeçalhos de registros e da estrutura física de árvores B. Criada para fornecer uma pequena verificação de sobrecarga da consistência física do grupo de arquivos, essa verificação também pode detectar páginas fragmentadas e falhas comuns de hardware que podem comprometer os dados. Uma execução completa de DBCC CHECKFILEGROUP pode demorar muito mais em versões anteriores. Esse comportamento ocorre devido às seguintes razões:  
 -   As verificações lógicas são mais abrangentes.  
 -   Algumas das estruturas subjacentes a serem verificadas são mais complexas.  
 -   Foram introduzidas muitas verificações novas para incluir os novos recursos.  
 Portanto, o uso da opção PHYSICAL_ONLY pode provocar um tempo de execução muito mais curto para DBCC CHECKFILEGROUP em grupos de arquivos grandes e, portanto, é recomendado para uso frequente em sistemas de produção. É recomendável ainda uma execução completa de DBCC CHECKFILEGROUP periodicamente. A frequência dessas execuções depende de fatores específicos aos negócios e ambientes de produção individuais. PHYSICAL_ONLY sempre implica em NO_INFOMSGS e não é permitido com nenhuma das opções de reparo.  
  
> [!NOTE]  
>  A especificação de PHYSICAL_ONLY faz com que DBCC CHECKFILEGROUP ignore todas as verificações de dados FILESTREAM.  
  
 MAXDOP  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 SP2 por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 Substitui o **grau máximo de paralelismo** opção de configuração de **sp_configure** para a instrução. O MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o administrador de recursos, o mecanismo de banco de dados usa o valor de MAXDOP do administrador de recursos, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!CAUTION]  
>  Se MAXDOP estiver definido como 0, o servidor escolherá o max degree of parallelism.  
  
## <a name="remarks"></a>Comentários  
DBCC CHECKFILEGROUP e DBCC CHECKDB são comandos DBCC semelhantes. A principal diferença é que DBCC CHECKFILEGROUP é limitado ao único grupo de arquivos especificado e às tabelas necessárias.
DBCC CHECKFILEGROUP executa os seguintes comandos:
-   [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) do grupo de arquivos.  
-   [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) de cada tabela e exibição indexada no grupo de arquivos.  
  
A execução de DBCC CHECKALLOC ou de DBCC CHECKTABLE separadamente de DBCC CHECKFILEGROUP não é necessária.
  
## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno  
DBCC CHECKFILEGROUP usa um instantâneo do banco de dados interno para fornecer a consistência transacional necessária ao executar essas verificações. Para obter mais informações, consulte [exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) e a seção "DBCC interno banco de dados uso de instantâneo" em [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Se um instantâneo não puder ser criado, ou se a opção TABLOCK for especificada, DBCC CHECKFILEGROUP irá adquirir bloqueios para obter a consistência necessária. Nesse caso, um bloqueio de banco de dados exclusivo é necessário para executar as verificações de alocação, e bloqueios de tabela compartilhados são necessários para executar as verificações de tabela. TABLOCK faz com que DBCC CHECKFILEGROUP seja executado com mais rapidez em um banco de dados sob carga pesada, mas reduz a simultaneidade disponível no banco de dados durante sua execução.
  
> [!NOTE]  
>  A execução de DBCC CHECKFILEGROUP em relação a tempdb não executa nenhuma verificação de alocação e deve adquirir bloqueios de tabela compartilhados para executar verificações de tabela. Isso porque, por razões de desempenho, instantâneos do banco de dados não estão disponíveis em tempdb. Isso significa que não é possível obter a consistência transacional exigida.  
  
## <a name="checking-objects-in-parallel"></a>Verificando objetos em paralelo  
Por padrão, DBCC CHECKFILEGROUP executa a verificação paralela de objetos. O grau de paralelismo é automaticamente determinado pelo processador de consulta. O grau de máximo de paralelismo é configurado da mesma forma que as consultas paralelas. Para restringir o número máximo de processadores disponíveis para a verificação DBCC, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
A verificação paralela pode ser desabilitada usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
  
## <a name="nonclustered-indexes-on-separate-filegroups"></a>Índices não clusterizados em grupos de arquivos separados  
Se um índice não clusterizado no grupo de arquivos especificado estiver associado a uma tabela em outro grupo de arquivos, o índice não é verificado porque a tabela base não está disponível para validação.
Se uma tabela no grupo de arquivos especificado tiver um índice não clusterizado em outro grupo de arquivos, o índice não clusterizado não será verificado por causa do seguinte:
-   A estrutura da tabela base não é dependente da estrutura de um índice não clusterizado. Os índices não clusterizados não precisam ser examinados para validar a tabela base.  
-   O comando DBCC CHECKFILEGROUP valida objetos somente no grupo de arquivos especificado.  
Um índice clusterizado e uma tabela não podem estar em grupos de arquivos diferentes; portanto as considerações anteriores se aplicam somente a índices não clusterizados.
  
## <a name="partitioned-tables-on-separate-filegroups"></a>Tabelas particionadas em grupos de arquivos separados  
Quando uma tabela particionada existe em vários grupos de arquivos, o DBCC CHECKFILEGROUP verifica os conjuntos de linhas de partição que existem no grupo de arquivos especificado e ignora os conjuntos de linhas nos outros grupos de arquivos. A mensagem informativa 2594 indica as partições que não foram verificadas. Índices não clusterizados não residentes no grupo de arquivos especificado não são verificados.
  
## <a name="understanding-dbcc-error-messages"></a>Compreendendo mensagens de erro DBCC  
Depois que o comando DBCC CHECKFILEGROUP é concluído, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará uma conclusão bem-sucedida e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação devido a um erro, a mensagem indica que o comando foi finalizado, um valor de estado e a quantidade de tempo de execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
  
|Estado|Description|  
|-----------|-----------------|  
|0|O número do erro 8930 foi gerado. Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|  
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|  
|3|Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|4|Uma declaração ou violação de acesso foi detectada.|  
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|  
  
## <a name="error-reporting"></a>Relatório de Erros  
Um arquivo de minidespejo (SQLDUMP*nnnn*. txt) é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório de LOG sempre que DBCC CHECKFILEGROUP detecta um erro de dano. Quando os recursos de coleta de dados Uso de Recursos e Relatório de Erros são habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo é encaminhado automaticamente à [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Os dados coletados são usados para aprimorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
O arquivo de despejo contém os resultados do comando DBCC CHECKFILEGROUP e saídas de diagnóstico adicionais. O arquivo tem DACLs (listas de controle de acesso discricionário) restritas. O acesso é limitado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta e membros de serviço a **sysadmin** função. Por padrão, o **sysadmin** função contém todos os membros do grupo BUILTIN\Administradores do Windows e o grupo de administradores locais. O comando DBCC não falhará se o processo de coleta de dados falhar.
  
## <a name="resolving-errors"></a>Resolvendo erros  
Se qualquer erro for informado por DBCC CHECKFILEGROUP, recomendamos a restauração do banco de dados com o backup de banco de dados. Observe que as opções de reparo não podem ser especificadas para DBCC CHECKFILEGROUP.
Se nenhum backup existir, a execução de DBCC CHECKDB com uma opção de reparo especificada corrige os erros relatados. A opção de reparo a ser usada será especificada no fim da lista se erros forem relatados. A correção de erros usando a opção REPAIR_ALLOW_DATA_LOSS pode exigir que algumas páginas e, portanto, dados, sejam excluídos.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC CHECKFILEGROUP retorna o seguinte conjunto de resultados (os valores podem variar):
-   Exceto quando ESTIMATEONLY ou NO_INFOMSGS é especificado.  
-   Para o banco de dados atual, se nenhum banco de dados estiver especificado, se todas as opções estiverem especificadas ou não (exceto NOINDEX).  
  
```sql
DBCC results for 'master'.  
DBCC results for 'sys.sysrowsetcolumns'.  
There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.  
DBCC results for 'sys.sysrowsets'.  
There are 97 rows in 1 pages for object 'sys.sysrowsets'.  
DBCC results for 'sysallocunits'.  
There are 195 rows in 3 pages for object 'sysallocunits'.  
  
There are 2340 rows in 16 pages for object 'spt_values'.  
DBCC results for 'MSreplication_options'.  
There are 2 rows in 1 pages for object 'MSreplication_options'.  
CHECKFILEGROUP found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Se NO_INFOMSGS estiver especificado, DBCC CHECKFILEGROUP retornará:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
 Se ESTIMATEONLY estiver especificado, DBCC CHECKFILEGROUP retornará (os valores podem variar):  

```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)
-------------------------------------------------   
15  
  
(1 row(s) affected)  
  
Estimated TEMPDB space needed for CHECKTABLES (KB)   
--------------------------------------------------   
207  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
### <a name="a-checking-the-primary-filegroup-in-the-a-database"></a>A. Verificando o grupo de arquivos PRIMARY de um banco de dados  
O exemplo a seguir verifica o grupo de arquivos primário do banco de dados atual.
  
```sql  
  
DBCC CHECKFILEGROUP;  
GO  
```  
  
### <a name="b-checking-the-adventureworks-primary-filegroup-without-nonclustered-indexes"></a>B. Verificando o grupo de arquivos PRIMARY de AdventureWorks sem índices não clusterizados  
A exemplo a seguir verifica o `AdventureWorks2012` banco de dados grupo de arquivos primário (excluindo índices não clusterizados) especificando o número de identificação do grupo de arquivos primário e especificando `NOINDEX`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKFILEGROUP (1, NOINDEX);  
GO  
```  
  
### <a name="c-checking-the-primary-filegroup-with-options"></a>C. Verificando o grupo de arquivos PRIMARY com opções  
O exemplo a seguir verifica o grupo de arquivos primário do banco de dados `master` e especifica a opção `ESTIMATEONLY`.
  
```sql  
USE master;  
GO  
DBCC CHECKFILEGROUP (1)  
WITH ESTIMATEONLY;  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[FILEGROUP_ID &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-id-transact-sql.md)  
[sp_helpfile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)  
[sp_helpfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)  
[sys. sysfilegroups &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysfilegroups-transact-sql.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKALLOC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)
  
  

