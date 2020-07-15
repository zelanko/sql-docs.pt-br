---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs:
- TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 4003b08205f1c7db98d2656e17fe653a3616638d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748950"
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Verifica a integridade lógica e física de todos os objetos do banco de dados especificado com a execução das seguintes operações:    
    
-   Executa [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) no banco de dados.    
-   Executa [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) em cada tabela e exibição no banco de dados.    
-   Executa [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md) no banco de dados.    
-   Valida o conteúdo de toda exibição indexada do banco de dados.    
-   Valida a consistência no nível do link entre arquivos e diretórios do sistema de arquivos e dos metadados de tabela ao armazenar dados **varbinary(max)** no sistema de arquivos usando FILESTREAM.    
-   Valida os dados [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados.    
    
Isso significa que os comandos DBCC CHECKALLOC, DBCC CHECKTABLE ou DBCC CHECKCATALOG não precisam ser executados separadamente do DBCC CHECKDB. Para obter informações mais detalhadas sobre as verificações executadas, consulte as descrições desses comandos.    
 
> [!NOTE]
> DBCC CHECKDB tem suporte em bancos de dados que contêm tabelas com otimização de memória, mas a validação ocorre apenas em tabelas baseadas em disco. No entanto, como parte do backup e recuperação de banco de dados, uma validação de CHECKSUM é feita para arquivos em grupos de arquivos com otimização de memória.    
>     
> Como as opções de reparo de DBCC não estão disponíveis para tabelas com otimização de memória, você deverá fazer o backup de seus bancos de dados regularmente e testar os backups. Se ocorrerem problemas de integridade de dados em uma tabela com otimização de memória, você deverá restaurar o último backup válido.    

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```syntaxsql
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>Argumentos    
 *database_name* | *database_id* | 0  
 É o nome ou a ID do banco de dados para o qual executar verificações de integridade. Se não for especificado ou se 0 for especificado, o banco de dados atual será usado. Os nomes de banco de dados precisam estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
    
NOINDEX  
 Especifica que não devem ser executadas verificações intensivas de índices não clusterizados de tabelas de usuário. Isto reduz o tempo de execução geral. NOINDEX não afeta tabelas do sistema porque as verificações de integridade sempre são executadas em todos os índices de tabela do sistema.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Especifica que DBCC CHECKDB repara os erros encontrados. Use as opções REPAIR apenas como um último recurso. O banco de dados especificado deve estar em modo de usuário único para usar uma das opções de reparo a seguir.  
    
REPAIR_ALLOW_DATA_LOSS  
 Tenta reparar todos os erros relatados. Esses reparos podem provocar alguma perda de dados.  
    
> [!WARNING]
> A opção REPAIR_ALLOW_DATA_LOSS é um recurso compatível, mas nem sempre é a melhor opção para colocar um banco de dados em um estado fisicamente consistente. Se for bem-sucedida, a opção REPAIR_ALLOW_DATA_LOSS poderá resultar em alguma perda de dados. Na verdade, ela pode resultar em mais dados perdidos do que se um usuário restaurar o banco de dados por meio do último backup válido. 
>
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] sempre recomenda uma restauração de usuário do último backup válido como o principal método de recuperação de erros relatados pelo DBCC CHECKDB. A opção REPAIR_ALLOW_DATA_LOSS não é uma alternativa para restaurar por meio de um backup válido. É uma opção emergencial de "último recurso" recomendada para uso somente se não for possível restaurar de um backup.    
>     
> Determinados erros, que só podem ser reparados usando a opção REPAIR_ALLOW_DATA_LOSS, podem envolver o deslocamento de uma linha, página ou série de páginas para limpar os erros. Qualquer dado desalocado não é mais acessível nem recuperável pelo usuário e o conteúdo exato dos dados desalocados não pode ser determinado. Portanto, a integridade referencial pode não ser precisa após a desalocação de linhas ou páginas porque as restrições de chave estrangeira não estão marcadas nem mantidas como parte da operação de reparo. O usuário deve verificar a integridade referencial do banco de dados (usando DBCC CHECKCONSTRAINTS) depois de usar a opção REPAIR_ALLOW_DATA_LOSS.    
>     
> Antes de executar o reparo, crie cópias físicas dos arquivos que pertencem a esse banco de dados. Isso inclui o arquivo de dados primário (.mdf), quaisquer arquivos de dados secundários (.ndf), todos os arquivos de log de transação (.ldf) e outros contêineres que formam o banco de dados incluindo catálogos de texto completo, pastas de fluxo de arquivos, dados de otimização de memória, etc.    
>     
> Antes de executar o reparo, considere alterar o estado do banco de dados para o modo de EMERGÊNCIA e tentar extrair o máximo possível de informações das tabelas críticas e salvar esses dados.    
    
REPAIR_FAST  
 Mantém a sintaxe apenas para compatibilidade com versões anteriores. Nenhuma ação de reparo é executada.  
    
REPAIR_REBUILD  
 Executa reparos que não têm nenhuma possibilidade de perda de dados. Isso pode incluir reparos rápidos, como reparo de linhas perdidas em índices não clusterizados e reparos mais demorados, como a recriação de um índice.  
 Esse argumento não repara erros que envolvem dados de FILESTREAM.  
    
> [!IMPORTANT] 
> Como DBCC CHECKDB com qualquer uma das opções REPAIR são completamente registrados e recuperáveis, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda sempre que um usuário use CHECKDB com quaisquer opções REPAIR em uma transação (execute BEGIN TRANSACTION antes de executar o comando) para que o usuário possa decidir se quer aceitar os resultados da operação. Em seguida, o usuário pode executar COMMIT TRANSACTION para confirmar todo o trabalho feito pela operação de reparo. Se o usuário não quiser aceitar os resultados da operação, ele poderá executar uma ROLLBACK TRANSACTION para desfazer os efeitos das operações de reparo.    
>     
> Para reparar erros, recomendamos restaurar de um backup. Operações de reparo não consideram nenhuma das restrições que podem existir em tabelas ou entre tabelas. Se a tabela especificada estiver envolvida em uma ou mais restrições, recomendamos executar DBCC CHECKCONSTRAINTS após uma operação de reparo. Se for necessário usar REPAIR, execute DBCC CHECKDB sem uma opção de reparo para localizar o nível de reparo a ser usado. Se você usar o nível de REPAIR_ALLOW_DATA_LOSS, recomendamos fazer backup do banco de dados antes de executar DBCC CHECKDB com essa opção.    
    
ALL_ERRORMSGS  
 Exibe todos os erros relatados por objeto. Todas as mensagens de erro são exibidas por padrão. Especificar ou omitir esta opção não têm nenhum efeito. As mensagens de erro são classificadas pela ID de objeto, exceto as mensagens geradas pelo [banco de dados tempdb](../../relational-databases/databases/tempdb-database.md).     

EXTENDED_LOGICAL_CHECKS  
 Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior, executará verificações de consistência lógica em uma exibição indexada, em índices XML e em índices espaciais, quando presentes.  
 Para obter mais informações, confira *Executando verificações de consistência lógica em índices*, na seção [Comentários](#remarks) mais adiante neste tópico.  
    
NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
    
TABLOCK  
 Faz com que DBCC CHECKDB obtenha bloqueios em vez de usar um instantâneo do banco de dados interno. Isso inclui um bloqueio exclusivo (X) de curto prazo no banco de dados. TABLOCK faz com que DBCC CHECKDB seja executado com mais rapidez em um banco de dados sob carga pesada, mas reduz a simultaneidade disponível no banco de dados durante sua execução.  
    
> [!IMPORTANT] 
> TABLOCK limita as verificações executadas, DBCC CHECKCATALOG não é executado no banco de dados e os dados do [!INCLUDE[ssSB](../../includes/sssb-md.md)] não são validados.
    
ESTIMATEONLY  
 Exibe a quantidade estimada de espaço no tempdb necessária para executar DBCC CHECKDB com todas as outras opções especificadas. A verificação real do banco de dados não é executada.  
    
PHYSICAL_ONLY  
 Limita a verificação à integridade da estrutura física da página e dos cabeçalhos de registros e a consistência da alocação do banco de dados. Essa verificação foi desenvolvida para fornecer uma pequena verificação de sobrecarga da consistência física do banco de dados, mas ela também pode detectar páginas interrompidas, falhas de soma de verificação e falhas comuns de hardware que podem comprometer os dados de um usuário.  
 A conclusão de uma execução completa de DBCC CHECKDB pode levar consideravelmente mais tempo do que em versões anteriores. Esse comportamento ocorre porque:  
 -   As verificações lógicas são mais abrangentes.  
 -   Algumas das estruturas subjacentes a serem verificadas são mais complexas.  
 -   Foram introduzidas muitas verificações novas para incluir os novos recursos.  
 Portanto, o uso da opção PHYSICAL_ONLY pode resultar em um tempo de execução muito mais curto de DBCC CHECKDB em grandes bancos de dados, e é recomendada para uso frequente em sistemas de produção. Ainda é recomendável executar um DBCC CHECKDB completo periodicamente. A frequência dessas execuções depende de fatores específicos aos negócios e ambientes de produção individuais.    
Este argumento sempre implica em NO_INFOMSGS e não é permitido com nenhuma das opções de reparo.  
    
> [!WARNING] 
> A especificação de PHYSICAL_ONLY faz com que DBCC CHECKDB ignore todas as verificações de dados FILESTREAM.
    
DATA_PURITY  
 Faz com que o DBCC CHECKDB verifique valores de colunas no banco de dados que não são válidos ou estão fora do intervalo. Por exemplo, o DBCC CHECKDB detecta colunas com valores de data e hora que são maiores ou menores do que o intervalo aceitável para o tipo de dados **datetime** ou **decimal** ou colunas de tipo de dados numérico aproximado com valores de escala ou de precisão que são inválidos.  
 Verificações de integridade de valor de coluna são habilitadas por padrão e não exigem a opção DATA_PURITY. Para bancos de dados atualizados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verificações de valores de colunas não são habilitadas por padrão até que o DBCC CHECKDB WITH DATA_PURITY tenha sido executado sem erros no banco de dados. Depois disso, DBCC CHECKDB verifica a integridade de valores de coluna por padrão. Para obter mais informações sobre como o CHECKDB pode ser afetado com a atualização de banco de dados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte a seção Comentários, posteriormente neste tópico.  
    
> [!WARNING]
> Se PHYSICAL_ONLY estiver especificado, não serão executadas verificações de integridade de colunas.
    
 Erros de validação relatados por essa opção não podem ser corrigidos usando opções de reparo de DBCC. Para obter informações sobre como corrigir esses erros manualmente, confira o artigo 923247 da Base de Dados de Conhecimento: [Solução de problemas do erro 2570 do DBCC no SQL Server 2005 e em versões posteriores](https://support.microsoft.com/kb/923247).  
    
 MAXDOP  
 **Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e posterior).  
    
 Substitui a opção de configuração **max degree of parallelism** de **sp_configure** da instrução. O MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o [!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)] usará o valor de MAXDOP do Resource Governor, descrito em [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
 
> [!WARNING] 
> Se MAXDOP estiver definido como zero, o SQL Server escolherá o grau máximo de paralelismo a ser usado.    

## <a name="remarks"></a>Comentários    
O DBCC CHECKDB não examina índices desabilitados. Para obter mais informações sobre índices desabilitados, confira [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).    

Se um tipo definido pelo usuário estiver marcado como sendo ordenado por byte, deverá existir apenas uma serialização do tipo definido pelo usuário. Se não houver uma serialização consistente de tipos definidos pelo usuário ordenados por byte, o erro 2537 ocorrerá quando DBCC CHECKDB for executado. Para obter mais informações, confira [Requisitos do tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md).    

Como o [Banco de dados de recursos](../../relational-databases/databases/resource-database.md) pode ser modificado apenas no modo de usuário único, o comando DBCC CHECKDB não pode ser executado diretamente nele. No entanto, quando DBCC CHECKDB é executado no [banco de dados mestre](../../relational-databases/databases/master-database.md), um segundo CHECKDB também é executado internamente no banco de dados de recursos. Isso significa que DBCC CHECKDB pode retornar resultados extras. O comando retorna conjuntos de resultados extras quando nenhuma opção está definida ou quando a opção `PHYSICAL_ONLY` ou `ESTIMATEONLY` está definida.    

Começando com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2, a execução de DBCC CHECKDB **não** limpa mais o cache de planos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2, a execução de DBCC CHECKDB limpava o cache de planos. A limpeza do cache do plano gera uma recompilação de todos os planos de execução posteriores e pode provocar uma queda repentina e temporária no desempenho da consulta. 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Executando verificações de consistência lógica em índices    
A verificação de consistência lógica em índices varia de acordo com o nível de compatibilidade do banco de dados, da seguinte maneira:
-   Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior:    
-   A menos que `NOINDEX` esteja especificado, DBCC CHECKDB executará verificações de consistência física e lógica em uma única tabela e em todos os índices não clusterizados. Entretanto, em índices XML, índices espaciais e exibições indexadas, por padrão são executadas somente as verificações de consistência física.
-   Se `WITH EXTENDED_LOGICAL_CHECKS` for especificado, verificações lógicas serão executadas em uma exibição indexada, índices XML e índices espaciais, quando presentes. Por padrão, as verificações de consistência física são executadas antes das verificações de consistência lógica. Se `NOINDEX` também estiver especificado, apenas as verificações lógicas serão executadas.
    
Essas verificações de consistência lógica comparam a tabela de índice interna do objeto de índice com a tabela do usuário à qual se está fazendo referência. Para localizar linhas externas, uma consulta interna é construída para executar uma interseção completa das tabelas internas e do usuário. A execução dessa consulta pode afetar bastante o desempenho e não é possível controlar seu andamento. Portanto, recomendamos especificar `WITH EXTENDED_LOGICAL_CHECKS` apenas se você suspeitar de problemas de índice que não estão relacionados à dano físico ou se as somas de verificação em nível de página foram desativadas e você suspeitar de dano de hardware em nível de coluna.
-   Se o índice for filtrado, DBCC CHECKDB executará verificações de consistência para verificar se as entradas do índice atendem ao predicado do filtro.
-   Se o nível de compatibilidade for 90 ou inferior, a menos que `NOINDEX` esteja especificado, DBCC CHECKDB executará verificações de consistência física e lógica em uma única tabela ou exibição indexada e em todos os índices XML e não clusterizados. Não há suporte para índices espaciais.  
- Começando com o SQL Server 2016, as verificações adicionais em colunas computadas persistentes, em colunas de UDT e em índices filtrados não são executadas por padrão, para evitar as avaliações de expressão caras. Essa alteração reduz significativamente a duração de CHECKDB em bancos de dados que contêm esses objetos. No entanto, as verificações de consistência física desses objetos sempre são concluídas. Somente quando a opção `EXTENDED_LOGICAL_CHECKS` for especificada as avaliações de expressão serão executadas além das verificações lógicas já presentes (exibição indexada, índices XML e índices espaciais) como parte da opção `EXTENDED_LOGICAL_CHECKS`.   
    
**Para saber o nível de compatibilidade de um banco de dados**
-   [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno    
DBCC CHECKDB usa um instantâneo do banco de dados interno para fornecer a consistência transacional necessária para executar essas verificações. Isso evita bloqueio e problemas de simultaneidade quando esses comandos são executados. Para obter mais informações, confira [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) e a seção Uso de instantâneo de banco de dados interno do DBCC em [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md). Se um instantâneo não puder ser criado, ou se a opção TABLOCK estiver especificada, DBCC CHECKDB irá adquirir bloqueios para obter a consistência necessária. Nesse caso, um bloqueio de banco de dados exclusivo é necessário para executar as verificações de alocação, e bloqueios de tabela compartilhados são necessários para executar as verificações de tabela.
O DBCC CHECKDB falhará ao ser executado no mestre quando não for possível criar um instantâneo do banco de dados interno.
A execução de DBCC CHECKDB no tempdb não executa nenhuma verificação de alocação nem de catálogo e precisa adquirir bloqueios de tabela compartilhada para executar verificações de tabela. Isso porque, por razões de desempenho, instantâneos do banco de dados não estão disponíveis em tempdb. Isso significa que não é possível obter a consistência transacional exigida.
No Microsoft SQL Server 2012 ou uma versão anterior do SQL Server, você pode encontrar mensagens de erro ao executar o comando DBCC CHECKDB para um banco de dados que tenha seus arquivos localizados em um volume formatado pelo ReFS. Para obter mais informações, confira o artigo 2974455 da base de dados de conhecimento: [Comportamento de DBCC CHECKDB quando o banco de dados do SQL Server está localizado em um volume ReFS.](https://support.microsoft.com/kb/2974455)    
    
## <a name="checking-and-repairing-filestream-data"></a>Verificando e reparando dados FILESTREAM    
Quando FILESTREAM está habilitado para um banco de dados e uma tabela, é possível armazenar opcionalmente BLOBs (objetos binários grandes) **varbinary(max)** no sistema de arquivos. Ao usar DBCC CHECKDB em um banco de dados que armazena BLOBs no sistema de arquivos, DBCC verifica a consistência em nível de vinculação entre o sistema de arquivos e o banco de dados.
Por exemplo, se uma tabela contiver uma coluna **varbinary(max)** que use o atributo FILESTREAM, o DBCC CHECKDB verificará se existe um mapeamento de um-para-um entre os diretórios e os arquivos do sistema de arquivos e entre as linhas e colunas da tabela e os valores das colunas. DBCC CHECKDB poderá reparar dano se você especificar a opção REPAIR_ALLOW_DATA_LOSS. Para reparar dano de FILESTREAM, o DBCC excluirá quaisquer linhas de tabela que não tiverem dados do sistema de arquivos.
    
## <a name="best-practices"></a>Práticas Recomendadas    
É recomendável usar a opção `PHYSICAL_ONLY` para uso frequente em sistemas de produção. O uso de PHYSICAL_ONLY pode reduzir significativamente o tempo de execução do DBCC CHECKDB em bancos de dados grandes. Também é recomendável executar DBCC CHECKDB periodicamente sem opções. A frequência dessas execuções depende das execuções de negócios individuais e de seus ambientes de produção.
    
## <a name="checking-objects-in-parallel"></a>Verificando objetos em paralelo    
Por padrão, DBCC CHECKDB executa a verificação paralela de objetos. O grau de paralelismo é automaticamente determinado pelo processador de consulta. O grau de máximo de paralelismo é configurado da mesma forma que as consultas paralelas. Para restringir o número máximo de processadores disponíveis para a verificação do DBCC, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). A verificação paralela pode ser desabilitada usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]
> Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte a verificação de consistência paralela na seção Gerenciamento do RDBMS de [Recursos compatíveis com as edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
    
## <a name="understanding-dbcc-error-messages"></a>Compreendendo mensagens de erro DBCC    
Depois que o comando DBCC CHECKDB é concluído, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará êxito e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação por causa de um erro, a mensagem indicará que o comando foi finalizado, um valor de estado e o tempo de execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
    
|Estado|Descrição|    
|-----------|-----------------|    
|0|O número do erro 8930 foi gerado. Isso indica um dano nos metadados que finalizou o comando DBCC.|    
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|    
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|    
|3|Isso indica um dano nos metadados que finalizou o comando DBCC.|    
|4|Uma declaração ou violação de acesso foi detectada.|    
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|    

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra a data e a hora em que uma verificação de consistência foi executada em um banco de dados sem erros (ou verificação de consistência "limpa"). Isso é conhecido como a `last known clean check`. Quando um banco de dados é iniciado pela primeira vez, essa data é gravada no EventLog (EventID-17573) e no ERRORLOG no seguinte formato: 
>
>`CHECKDB for database '<database>' finished without errors on 2019-05-05 18:08:22.803 (local time). This is an informational message only; no user action is required.`
    

## <a name="error-reporting"></a>Relatório de Erros    
Um arquivo de despejo (`SQLDUMP*nnnn*.txt`) é criado no diretório LOG do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre que DBCC CHECKDB detecta um erro de corrupção. Quando a coleta de dados *Uso de Recursos* e os recursos de *Relatório de Erros* recursos estão habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo é encaminhado automaticamente ao [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Os dados coletados são usados para aprimorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
O arquivo de despejo contém os resultados do comando DBCC CHECKDB e saídas de diagnóstico adicionais. O acesso é limitado à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aos membros da função sysadmin. Por padrão, a função de sysadmin contém todos os membros do grupo `BUILTIN\Administrators` do Windows e do grupo do administrador local. O comando DBCC não falhará se o processo de coleta de dados falhar.
    
## <a name="resolving-errors"></a>Resolvendo erros    
Se qualquer erro for relatado pelo DBCC CHECKDB, é recomendável restaurar o banco de dados do backup em vez de executar REPAIR com uma das opções de REPAIR. Se não existir nenhum backup, a execução de REPAIR corrigirá os erros relatados. A opção de reparo a ser usada é especificada no fim da lista de erros relatados. No entanto, a correção de erros usando a opção REPAIR_ALLOW_DATA_LOSS pode exigir que algumas páginas e, portanto, alguns dados, sejam excluídos.    

Em determinadas circunstâncias, podem ser inseridos valores no banco de dados que são inválidos ou estão fora do intervalo baseado no tipo de dados da coluna. O DBCC CHECKDB pode detectar valores de coluna inválidos para todos os tipos de dados de colunas. Portanto, a execução de DBCC CHECKDB com a opção DATA_PURITY em bancos de dados que foram atualizados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode revelar erros preexistentes de valores de colunas. Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode reparar estes erros automaticamente, o valor da coluna deve ser atualizado manualmente. Se o CHECKDB detectar esse tipo de erro, ele retornará um aviso, o erro número 2570 e informações para identificar a linha afetada e corrigir o erro manualmente.    

O reparo pode ser executado sob uma transação do usuário para permitir que o usuário reverta as alterações feitas. Se reparos forem revertidos, o banco de dados ainda conterá erros e deverá ser restaurado de um backup. Depois de concluir os reparos, faça um backup do banco de dados.
    
## <a name="resolving-errors-in-database-emergency-mode"></a>Resolvendo erros no modo de emergência do banco de dados    
Quando um banco de dados tiver sido configurado como modo de emergência com a instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md), o DBCC CHECKDB poderá executar alguns reparos especiais no banco de dados se a opção REPAIR_ALLOW_DATA_LOSS estiver especificada. Esses reparos podem permitir que bancos de dados geralmente irrecuperáveis sejam colocados online em um estado fisicamente consistente. Esses reparos devem ser usados como um último recurso e apenas quando não for possível restaurar o banco de dados de um backup. Quando o banco de dados estiver definido como modo de emergência, o banco dedados será marcado como READ_ONLY, o registro em log será desabilitado e o acesso será limitado aos membros da função de servidor fixa sysadmin.
    
> [!NOTE]
> Não é possível executar o comando DBCC CHECKDB em modo de emergência dentro de uma transação de usuário e reverter a transação após a execução.    
    
Quando o banco de dados está em modo de emergência e DBCC CHECKDB com a cláusula REPAIR_ALLOW_DATA_LOSS é executada, as seguintes ações são executadas:
-   O DBCC CHECKDB usa páginas que foram marcadas como inacessíveis devido a erros de E/S ou de soma de verificação, como se os erros não tivessem ocorrido. Isso aumenta as chances de recuperação de dados do banco de dados.    
-   O DBCC CHECKDB tenta recuperar o banco de dados usando técnicas normais de recuperação baseadas em log.    
-   Se, devido a danos no log de transações, a recuperação do banco de dados não tiver êxito, o log de transações será reconstruído. A reconstrução do log de transações pode resultar na perda de consistência transacional.    
    
> [!WARNING]
> A opção REPAIR_ALLOW_DATA_LOSS é um recurso com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, não sempre é a melhor opção para colocar um banco de dados em um estado fisicamente consistente. Se for bem-sucedida, a opção REPAIR_ALLOW_DATA_LOSS poderá resultar em alguma perda de dados. Na verdade, ela pode resultar em mais dados perdidos do que se um usuário restaurar o banco de dados por meio do último backup válido. [!INCLUDE[msCoName](../../includes/msconame-md.md)] sempre recomenda uma restauração de usuário do último backup válido como o principal método de recuperação de erros relatados pelo DBCC CHECKDB. A opção REPAIR_ALLOW_DATA_LOSS **não** é uma alternativa para a restauração de um backup realmente válido. É uma opção emergencial de "último recurso" recomendada para uso somente se não for possível restaurar de um backup.    
>     
>  Depois de recriar o log, não há nenhuma garantia ACID completa.    
>     
>  Depois de recriar o log, o DBCC CHECKDB será executado automaticamente e relatará e corrigirá problemas de consistência física.    
>     
>  Restrições de consistência de dados lógicos e lógica de negócios imposta devem ser validadas manualmente.    
>     
>  O tamanho do log de transação será deixado ao seu tamanho padrão e deve ser ajustado manualmente para o tamanho recente.    
    
Se o comando DBCC CHECKDB for bem-sucedido, o banco de dados estará em um estado fisicamente consistente e o status do banco de dados será definido como ONLINE. No entanto, o banco de dados poderá conter uma ou mais inconsistências transacionais. É recomendável executar o [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) para identificar qualquer falha na lógica de negócios e fazer backup do banco de dados imediatamente.
Se o comando DBCC CHECKDB falhar, o banco de dados não poderá ser reparado.
    
## <a name="running-dbcc-checkdb-with-repair_allow_data_loss-in-replicated-databases"></a>Executando DBCC CHECKDB com REPAIR_ALLOW_DATA_LOSS em bancos de dados replicados    
A execução do comando DBCC CHECKDB com a opção REPAIR_ALLOW_DATA_LOSS pode afetar bancos de dados de usuário (bancos de dados de publicação e assinatura) e o banco de dados de distribuição usado pela replicação. Bancos de dados de publicação e assinatura incluem tabelas publicadas e tabelas de metadados de replicação. Fique atento aos seguintes problemas potenciais nesses bancos de dados:
-   Tabelas publicadas. Ações executadas pelo processo CHECKDB para reparar dados de usuário corrompidos podem não ser replicadas:    
-   A replicação de mesclagem usa gatilhos para controlar alterações em tabelas publicadas. Se linhas forem inseridas, atualizadas ou excluídas pelo processo CHECKDB, os gatilhos não serão disparados. Portanto a alteração não será replicada.
-   A replicação transacional usa o log de transações para controlar alterações em tabelas publicadas. Em seguida, o Log Reader Agent move essas alterações para o banco de dados de distribuição. Alguns reparos do DBCC, embora sejam registrados, não podem ser replicados pelo Log Reader Agent. Por exemplo, se uma página de dados for desalocada pelo processo CHECKDB, o Log Reader Agent não converterá isso em uma instrução DELETE. Portanto a alteração não será replicada.
-   Tabelas de metadados de replicação. Ações executadas pelo processo CHECKDB para reparar tabelas de metadados de replicação corrompidas exigeem a remoção e a reconfiguração da replicação.    
    
Se você precisar executar o comando DBCC CHECKDB com a opção REPAIR_ALLOW_DATA_LOSS em um banco de dados de usuário ou de distribuição:
1.  Pare o sistema: Pare as atividades do banco de dados e de todos os outros bancos de dados da topologia da replicação e tente sincronizar todos os nós. Para obter mais informações, consulte [Como confirmar uma topologia de replicação &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).    
1.  Execute DBCC CHECKDB.    
1.  Se o relatório do DBCC CHECKDB incluir reparos de qualquer tabela no banco de dados de distribuição ou de qualquer tabela de metadados de replicação em um banco de dados de usuário, remova e reconfigure a replicação. Para obter mais informações, consulte [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md).    
1.  Se o relatório do DBCC CHECKDB incluir reparos de qualquer tabela replicada, execute validação de dados para determinar se existem diferenças entre os dados do banco de dados de publicação e de assinatura.    
    
## <a name="result-sets"></a>Conjuntos de resultados    
O DBCC CHECKDB retorna o conjunto de resultados a seguir. Os valores podem variar exceto quando as opções ESTIMATEONLY, PHYSICAL_ONLY ou NO_INFOMSGS estiverem especificadas:
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

O DBCC CHECKDB retorna o conjunto de resultados (mensagem) a seguir quando NO_INFOMSGS está especificado:
    
```
 The command(s) completed successfully.
 ```
 
O DBCC CHECKDB retorna o conjunto de resultados a seguir quando PHYSICAL_ONLY está especificado:
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
O DBCC CHECKDB retorna o conjunto de resultados a seguir quando ESTIMATEONLY está especificado.
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>Permissões    
Requer associação à função de servidor fixa sysadmin ou à função de banco de dados fixa db_owner.
    
## <a name="examples"></a>Exemplos    
    
### <a name="a-checking-both-the-current-and-another-database"></a>a. Verificando os bancos de dados atual e outro banco de dados    
O exemplo a seguir executa `DBCC CHECKDB` para o banco de dados atual e o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. Verificando o banco de dados atual, suprimindo mensagens informativas    
O exemplo a seguir verifica o banco de dados atual e suprime todas as mensagens informativas.
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>Consulte Também    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

