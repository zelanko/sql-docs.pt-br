---
title: DBCC CHECKTABLE (Transact-SQL) | Microsoft Docs
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKTABLE_TSQL
- DBCC_CHECKTABLE_TSQL
- DBCC CHECKTABLE
- CHECKTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], DBCC CHECKTABLE
- page integrity checks [SQL Server]
- consistency [SQL Server], tables
- consistency [SQL Server], indexed views
- DBCC CHECKTABLE statement
- integrity [SQL Server]
- low overhead checks
- table integrity checks [SQL Server]
ms.assetid: 0d6cb620-eb58-4745-8587-4133a1b16994
caps.latest.revision: 89
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af19e042e9e40bd92352a175394c442431959b0e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checktable-transact-sql"></a>DBCC CHECKTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Verifica a integridade de todas as páginas e estruturas que compõem a tabela ou exibição indexada.
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
    
## <a name="syntax"></a>Sintaxe    
    
```sql
    
DBCC CHECKTABLE     
(    
    table_name | view_name    
    [ , { NOINDEX | index_id }    
     |, { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD }     
    ]     
)    
    [ WITH     
        { ALL_ERRORMSGS ]    
          [ , EXTENDED_LOGICAL_CHECKS ]     
          [ , NO_INFOMSGS ]    
          [ , TABLOCK ]     
          [ , ESTIMATEONLY ]     
          [ , { PHYSICAL_ONLY | DATA_PURITY } ]     
          [ , MAXDOP = number_of_processors ]    
        }    
    ]    
```    
    
## <a name="arguments"></a>Argumentos    
 *table_name* | *view_name*  
 É a tabela ou exibição indexada para a qual executar verificações de integridade. Nomes de tabela ou exibição devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
    
 NOINDEX  
 Especifica que não devem ser executadas verificações intensivas de índices não clusterizados de tabelas de usuário. Isto reduz o tempo de execução geral. NOINDEX não afeta tabelas do sistema porque as verificações de integridade sempre são executadas em todos os índices de tabela do sistema.  
    
 *index_id*  
 É o número da ID (identificação) do índice para o qual executar verificações de integridade. Se *index_id* for especificado, DBCC CHECKTABLE executará verificações de integridade naquele índice, junto com o heap ou índice clusterizado.  
    
 REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Especifica que DBCC CHECKTABLE repara os erros encontrados. Para usar uma opção de reparo, o banco de dados deve estar em modo de usuário único.  
    
 REPAIR_ALLOW_DATA_LOSS  
 Tenta reparar todos os erros relatados. Esses reparos podem provocar alguma perda de dados.  
    
 REPAIR_FAST  
 A sintaxe é mantida apenas para compatibilidade com versões anteriores. Nenhuma ação de reparo é executada.  
    
 REPAIR_REBUILD  
 Executa reparos que não têm nenhuma possibilidade de perda de dados. Isso pode incluir reparos rápidos, como reparo de linhas perdidas em índices não clusterizados e reparos mais demorados, como a recriação de um índice.  
 Esse argumento não repara erros que envolvem dados FILESTREAM.  
    
 > [!NOTE]  
 >  Use as opções REPAIR apenas como um último recurso. Para reparar erros, recomendamos restaurar de um backup. Operações de reparo não consideram nenhuma das restrições que podem existir em tabelas ou entre tabelas. Se a tabela especificada estiver envolvida em uma ou mais restrições, recomendamos executar DBCC CHECKCONSTRAINTS após uma operação de reparo. Se for necessário usar REPAIR, execute DBCC CHECKTABLE sem uma opção de reparo para localizar o nível de reparo a ser usado. Se você pretende usar o nível de REPAIR_ALLOW_DATA_LOSS, é recomendável fazer backup do banco de dados antes de executar DBCC CHECKTABLE com essa opção.  
    
 ALL_ERRORMSGS  
 Exibe um número ilimitado de erros. Todas as mensagens de erro são exibidas por padrão. Especificar ou omitir esta opção não têm nenhum efeito.  
    
 EXTENDED_LOGICAL_CHECKS  
 Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior, executará verificações de consistência lógica em uma exibição indexada, índices XML e índices espaciais, quando presentes.  
 Para obter mais informações, consulte "Executando verificações de consistência lógica em índices" na seção "Comentários" deste tópico.  
    
 NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
    
 TABLOCK  
 Faz com que DBCC CHECKTABLE obtenha um bloqueio de tabela compartilhada em vez de usar um instantâneo do banco de dados interno. TABLOCK faz com que DBCC CHECKTABLE seja executado com mais rapidez em uma tabela sob carga pesada, mas reduz a simultaneidade disponível na tabela durante a execução de DBCC CHECKTABLE.  
    
 ESTIMATEONLY  
 Exibe a quantidade estimada de espaço em tempdb necessária para executar DBCC CHECKTABLE com todas as outras opções especificadas.  
    
 PHYSICAL_ONLY  
 Limita a verificação à integridade da estrutura física da página, dos cabeçalhos de registros e da estrutura física de árvores B. Criada para fornecer uma pequena verificação de sobrecarga da consistência física da tabela, essa verificação também pode detectar páginas interrompidas e falhas comuns de hardware que podem comprometer os dados. Uma execução completa de DBCC CHECKTABLE pode demorar muito mais em versões anteriores. Esse comportamento ocorre devido às seguintes razões:  
 -   As verificações lógicas são mais abrangentes.  
 -   Algumas das estruturas subjacentes a serem verificadas são mais complexas.  
 -   Foram introduzidas muitas verificações novas para incluir os novos recursos.  
   
 O uso da opção PHYSICAL_ONLY pode provocar um tempo de execução muito mais curto para DBCC CHECKTABLE em tabelas grandes. Portanto é recomendado para uso frequente em sistemas de produção. Ainda é recomendável executar um DBCC CHECKTABLE completo periodicamente. A frequência dessas execuções depende de fatores específicos aos negócios e ambientes de produção individuais. PHYSICAL_ONLY sempre implica em NO_INFOMSGS e não é permitido com nenhuma das opções de reparo.  
    
 > [!NOTE]  
 >  A especificação de PHYSICAL_ONLY faz com que DBCC CHECKTABLE ignore todas as verificações de dados FILESTREAM.  
    
 DATA_PURITY  
 Faz com que o DBCC CHECKTABLE verifique valores de colunas na tabela que não são válidos ou estão fora do intervalo. Por exemplo, DBCC CHECKTABLE detecta colunas com valores de data e hora que são maiores ou menores do que o intervalo aceitável para o **datetime** tipo de dados; ou **decimal** ou tipo de dados numérico aproximado colunas com valores de escala ou precisão que não são válidos.  
 Verificações de integridade de valor de coluna são habilitadas por padrão e não exigem a opção DATA_PURITY. Para bancos de dados atualizados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível usar DBCC CHECKTABLE WITH DATA_PURITY para localizar e corrigir erros em uma tabela específica. No entanto verificações de valores de colunas na tabela não são habilitadas por padrão até que o DBCC CHECKDB WITH DATA_PURITY tenha sido executado sem erros no banco de dados. Depois disto, por padrão, DBCC CHECKDB e DBCC CHECKTABLE verificam a integridade de valores de colunas.  
 Erros de validação relatados por essa opção não podem ser corrigidos usando opções de reparo de DBCC. Para obter informações sobre como corrigir esses erros manualmente, consulte o artigo 923247 da Base de dados de Conhecimento: [Troubleshooting DBCC error 2570 no SQL Server 2005 e versões posteriores](http://support.microsoft.com/kb/923247).  
 Se PHYSICAL_ONLY estiver especificado, não serão executadas verificações de integridade de colunas.  
    
 MAXDOP  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 SP2 por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
 Substitui o **grau máximo de paralelismo** opção de configuração de **sp_configure** para a instrução. O MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o administrador de recursos, o mecanismo de banco de dados usa o valor de MAXDOP do administrador de recursos, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
    
 > [!CAUTION]  
 >  Se MAXDOP estiver definido como 0, o servidor escolherá o max degree of parallelism.  
    
## <a name="remarks"></a>Comentários    
    
> [!NOTE]    
>  Para executar DBCC CHECKTABLE em cada tabela no banco de dados, use [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).    
    
Para a tabela especificada, DBCC CHECKTABLE verifica o seguinte:
-   Páginas de dados de estouro de linha, índice, em linha e LOB estão vinculadas corretamente.    
-   Os índices estão na ordem de classificação correta.    
-   Os ponteiros são consistentes.    
-   Os dados em cada página são razoáveis, inclusive colunas computadas.    
-   Deslocamentos de página são razoáveis.    
-   Cada linha da tabela base tem uma linha correspondente em cada índice não clusterizado e vice-versa.    
-   Cada linha de um índice ou tabela particionada está na partição correta.    
-   Link de nível de consistência entre o sistema de arquivos e a tabela ao armazenar **varbinary (max)** dados no sistema de arquivos usando FILESTREAM.    
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Executando verificações de consistência lógica em índices    
A verificação de consistência lógica em índices varia de acordo com o nível de compatibilidade do banco de dados, da seguinte maneira:
-   Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior:    
    -   A menos que NOINDEX esteja especificado, DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela e em todos os índices não clusterizados. Entretanto, em índices XML, índices espaciais e exibições indexadas, por padrão são executadas somente as verificações de consistência física.    
    -   Se WITH EXTENDED_LOGICAL_CHECKS estiver especificado, verificações lógicas serão executadas em uma exibição indexada, em índices XML e em índices espaciais, quando presentes. Por padrão, as verificações de consistência física são executadas antes das verificações de consistência lógica. Se NOINDEX também estiver especificado, apenas as verificações lógicas serão executadas.    
         Essas verificações de consistência lógica comparam a tabela de índice interna do objeto de índice com a tabela do usuário à qual se está fazendo referência. Para localizar linhas externas, uma consulta interna é construída para executar uma interseção completa das tabelas internas e do usuário. A execução dessa consulta pode afetar bastante o desempenho e não é possível controlar seu andamento. Portanto, recomendamos especificar WITH EXTENDED_LOGICAL_CHECKS apenas se você suspeitar de problemas de índice que não estão relacionados à dano físico ou se as somas de verificação em nível de página foram desativadas e você suspeitar de dano de hardware em nível de coluna.    
    -   Se o índice for filtrado, DBCC CHECKDB executará verificações de consistência para verificar se as entradas do índice atendem ao predicado do filtro.   
      
- Começando com o SQL Server 2016, verificações adicionais em colunas computadas persistentes, colunas de UDT e índices filtrados não serão executado por padrão para evitar as avaliações de expressão caro. Essa alteração reduz significativamente a duração de CHECKDB em bancos de dados que contêm esses objetos. No entanto, as verificações de consistência física desses objetos sempre é executado. Somente quando a opção EXTENDED_LOGICAL_CHECKS estiver especificada serão avaliações de expressão executadas além dos já presentes verificações lógicas (exibição indexada, índices XML e índices espaciais) como parte da opção EXTENDED_LOGICAL_CHECKS.
-  Se o nível de compatibilidade for 90 ou inferior, a menos que NOINDEX esteja especificado, DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela ou exibição indexada e em todos os índices XML e não clusterizados. Não há suporte para índices espaciais.
    
 **Para saber o nível de compatibilidade do banco de dados**    
[Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno    
DBCC CHECKTABLE usa um instantâneo do banco de dados interno para fornecer a consistência transacional necessária ao executar essas verificações. Para obter mais informações, consulte [exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) e a seção "DBCC interno banco de dados uso de instantâneo" em [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Se um instantâneo não puder ser criado, ou se a opção TABLOCK estiver especificada, DBCC CHECKTABLE irá adquirir um bloqueio de tabela compartilhada para obter a consistência necessária.
    
> [!NOTE]    
> Se DBCC CHECKTABLE for executado em tempdb, ele deverá adquirir um bloqueio de tabela compartilhada. Isso porque, por razões de desempenho, instantâneos do banco de dados não estão disponíveis em tempdb. Isso significa que não é possível obter a consistência transacional exigida.    
    
## <a name="checking-and-repairing-filestream-data"></a>Verificando e reparando dados FILESTREAM    
Quando FILESTREAM está habilitado para um banco de dados e uma tabela, você pode opcionalmente armazenar **varbinary (max)** objetos binários grandes (BLOBs) no sistema de arquivos. Ao usar DBCC CHECKTABLE em uma tabela que armazena BLOBs no sistema de arquivos, DBCC verifica a consistência em nível de vinculação entre o sistema de arquivos e o banco de dados.
Por exemplo, se uma tabela contiver uma **varbinary (max)** coluna que usa o atributo FILESTREAM, DBCC CHECKTABLE verificará se há um mapeamento um para um entre diretórios do sistema de arquivos e arquivos e linhas da tabela, colunas e colunas valores. DBCC CHECKTABLE poderá reparar dano se você especificar a opção REPAIR_ALLOW_DATA_LOSS. Para reparar danos de FILESTREAM, o DBCC excluirá todas as linhas da tabela que não têm dados do sistema de arquivos e excluirá todos os diretórios e arquivos que não são mapeados para uma linha de tabela, coluna ou valor de coluna.
    
## <a name="checking-objects-in-parallel"></a>Verificando objetos em paralelo    
Por padrão, DBCC CHECKTABLE executa a verificação paralela de objetos. O grau de paralelismo é automaticamente determinado pelo processador de consulta. O grau máximo de paralelismo é configurado da mesma maneira como o de consultas paralelas. Para restringir o número máximo de processadores disponíveis para a verificação DBCC, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
A verificação paralela pode ser desabilitada usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]    
>  Durante uma operação de DBCC CHECKTABLE, os bytes armazenados em uma coluna de tipo definido pelo usuário, ordenada por byte, devem ser iguais aos da serialização computada do valor do tipo definido pelo usuário. Se isto não for verdadeiro, a rotina de DBCC CHECKTABLE relatará um erro de consistência.    
    
## <a name="understanding-dbcc-error-messages"></a>Compreendendo mensagens de erro DBCC    
Depois que o comando DBCC CHECKTABLE é concluído, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará uma conclusão bem-sucedida e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação devido a um erro, a mensagem indica que o comando foi finalizado, um valor de estado e a quantidade de tempo de execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
    
|Estado|Description|    
|-----------|-----------------|    
|0|O número do erro 8930 foi gerado. Isso indica um dano de metadados que provocou a finalização do comando DBCC.|    
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|    
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|    
|3|Isso indica um dano de metadados que provocou a finalização do comando DBCC.|    
|4|Uma declaração ou violação de acesso foi detectada.|    
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|    
    
## <a name="error-reporting"></a>Relatório de Erros    
Um arquivo de minidespejo (SQLDUMP*nnnn*. txt) é criado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório de LOG sempre que DBCC CHECKTABLE detecta um erro de dano. Quando os recursos de coleta de dados Uso de Recursos e Relatório de Erros são habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo é encaminhado automaticamente à [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Os dados coletados são usados para aprimorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
O arquivo de despejo contém os resultados do comando DBCC CHECKTABLE e saídas de diagnóstico adicionais. O arquivo tem DACLs (listas de controle de acesso discricionário) restritas. O acesso é limitado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] membros da função sysadmin e conta de serviço. Por padrão, a função de sysadmin contém todos os membros do grupo BUILTIN\Administradores do Windows e o grupo de administradores locais. O comando DBCC não falhará se o processo de coleta de dados falhar.
    
## <a name="resolving-errors"></a>Resolvendo erros    
 Se qualquer erro for relatado pelo DBCC CHECKTABLE, recomendamos a restauração do banco de dados do backup em vez da execução de REPAIR com uma das opções REPAIR. Se não existir nenhum backup, a execução de REPARAR poderá corrigir os erros relatados. A opção REPAIR a ser usada é especificada no fim da lista de erros relatados. No entanto, a correção dos erros usando a opção REPAIR_ALLOW_DATA_LOSS pode exigir que algumas páginas e, portanto, dados, sejam excluídos.    
O reparo pode ser executado sob uma transação do usuário para permitir que o usuário reverta as alterações feitas. Se reparos forem revertidos, o banco de dados ainda conterá erros e deverá ser restaurado de um backup. Depois de concluir todos os reparos, faça backup do banco de dados.
    
## <a name="result-sets"></a>Conjuntos de resultados    
O DBCC CHECKTABLE retorna o seguinte conjunto de resultados. O mesmo conjunto de resultados será retornado se você especificar apenas o nome da tabela ou qualquer uma das opções.
    
```sql
DBCC results for 'HumanResources.Employee'.    
There are 288 rows in 13 pages for object 'Employee'.    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
O DBCC CHECKTABLE retornará o conjunto de resultados a seguir se a opção de ESTIMATEONLY for especificada:
    
```sql
Estimated TEMPDB space needed for CHECKTABLES (KB)     
--------------------------------------------------     
21    
(1 row(s) affected)    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
## <a name="permissions"></a>Permissões    
Usuário deve possuir a tabela ou ser membro da função de servidor fixa sysadmin, db_owner fixa função de banco de dados ou da função de banco de dados fixa db_ddladmin.    
    
## <a name="examples"></a>Exemplos    
    
### <a name="a-checking-a-specific-table"></a>A. Verificando uma tabela específica    
O exemplo a seguir verifica a integridade de página dos dados de `HumanResources.Employee` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee');    
GO    
```    
    
### <a name="b-performing-a-low-overhead-check-of-the-table"></a>B. Executando uma verificação de sobrecarga baixa da tabela    
 O exemplo a seguir executa uma verificação de sobrecarga baixa do `Employee` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.    
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee') WITH PHYSICAL_ONLY;    
GO    
```    
    
### <a name="c-checking-a-specific-index"></a>C. Verificando um índice específico    
 O exemplo a seguir verifica um índice específico obtido por meio de acesso a `sys.indexes`.    
    
```sql    
DECLARE @indid int;    
SET @indid = (SELECT index_id     
              FROM sys.indexes    
              WHERE object_id = OBJECT_ID('Production.Product')    
                    AND name = 'AK_Product_Name');    
DBCC CHECKTABLE ('Production.Product',@indid);    
```    
    
## <a name="see-also"></a>Consulte também    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)    
    
  

