---
title: ALTER DATABASE de arquivo e grupo de arquivos
description: Atualize os arquivos e grupos de arquivo de um banco de dados usando o Transact-SQL.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e4a00b8bff85625cf48f8ba1f5abf3fb14ce94a8
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113241"
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>Opções de arquivo e grupos de arquivos de ALTER DATABASE (Transact-SQL)

Modifica os arquivos e grupos de arquivos associados ao banco de dados. Adiciona ou remove arquivos e grupos de arquivos de um banco de dados e altera os atributos de um banco de dados ou seus arquivos e grupos de arquivos. Para obter outras opções de ALTER DATABASE, confira [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Instância gerenciada<br />do Banco de Dados SQL](alter-database-transact-sql-file-and-filegroup-options.md?view=azuresqldb-mi-current)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="syntax"></a>Sintaxe

```syntaxsql
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | ADD LOG FILE <filespec> [ ,...n ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}

<filespec>::=
(
    NAME = logical_file_name
    [ , NEWNAME = new_logical_name ]
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
    [ , OFFLINE ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>Argumentos

**\<add_or_modify_files>::=**

Especifica o arquivo a ser adicionado, removido ou modificado.

*database_name* É o nome do banco de dados a ser modificado.

ADD FILE Adiciona um arquivo ao banco de dados.

TO FILEGROUP { *filegroup_name* } Especifica o grupo de arquivos ao qual adicionar o arquivo especificado. Para exibir os grupos de arquivos atuais e qual grupo de arquivos é o padrão atual, use a exibição do catálogo [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).

ADD LOG FILE Adiciona um arquivo de log ao banco de dados especificado.

REMOVE FILE *logical_file_name* Remove a descrição do arquivo lógico de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui o arquivo físico. O arquivo não pode ser removido, a menos que esteja vazio.

*logical_file_name* É o nome lógico usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao fazer referência ao arquivo.

> [!WARNING]
> A remoção de um arquivo de banco de dados que tem backups de `FILE_SNAPSHOT` associados a ele terá êxito, mas os instantâneos associados não serão excluídos para evitar a anulação dos backups que referenciam o arquivo de banco de dados. O arquivo será truncado, mas não será fisicamente excluído para manter os backups de FILE_SNAPSHOT intactos. Para obter mais informações, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

MODIFY FILE Especifica o arquivo que deve ser modificado. Apenas uma propriedade \<filespec> pode ser alterada por vez. NAME sempre deve ser especificado em \<filespec> para identificar o arquivo a ser modificado. Se SIZE for especificado, o novo tamanho deverá ser maior que o tamanho do arquivo atual.

Para modificar o nome lógico de um arquivo de dados ou de um arquivo de log, especifique o nome do arquivo lógico a ser renomeado na cláusula `NAME` e especifique o novo nome lógico para o arquivo na cláusula `NEWNAME`. Por exemplo:

```sql
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )
```

Para mover um arquivo de dados ou de log para um novo local, especifique o nome do arquivo lógico atual na cláusula `NAME` e especifique o novo caminho e o nome do arquivo do sistema operacional na cláusula `FILENAME`. Por exemplo:

```sql
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )
```

Quando você move um catálogo de texto completo, especifique somente o novo caminho na cláusula FILENAME. Não especifique o nome do arquivo do sistema operacional.

Para obter mais informações, consulte [Mover arquivos de bancos de dados](../../relational-databases/databases/move-database-files.md).

Para um grupo de arquivos FILESTREAM, NAME pode ser modificado online. FILENAME pode ser modificado online; entretanto, a operação não entra em vigor até que o contêiner seja fisicamente realocado e o servidor seja desligado e reiniciado.

Você pode definir um arquivo FILESTREAM como OFFLINE. Quando um arquivo FILESTREAM estiver offline, seu grupo de arquivos pai será internamente marcado como offline; portanto, haverá falha em todo acesso aos dados FILESTREAM naquele grupo de arquivos.

> [!NOTE]
> As opções \<add_or_modify_files> não estão disponíveis em um Banco de Dados Independente.

**\<filespec>::=**

Controla as propriedades do arquivo.

NAME *logical_file_name* Especifica o nome lógico do arquivo.

*logical_file_name* É o nome lógico usado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao referenciar o arquivo.

NEWNAME *new_logical_file_name* Especifica um novo nome lógico para o arquivo.

*new_logical_file_name* É o nome para substituir o nome de arquivo lógico existente. O nome deve ser exclusivo dentro do banco de dados e obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md). O nome pode ser uma constante de caractere ou Unicode, um identificador comum ou delimitado.

FILENAME { **'** _os\_file\_name_ **'** | **'** _filestream\_path_ **'** | **'** _memory\_optimized\_data\_path_ **'** } Especifica o nome de arquivo (físico) do sistema operacional.

' *os_file_name* ' Para um grupo de arquivos padrão (ROWS), esse é o caminho e o nome do arquivo usado pelo sistema operacional quando você cria o arquivo. O arquivo deve residir no servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. O caminho especificado deve existir antes da execução da instrução ALTER DATABASE.

> [!NOTE]
> Os parâmetros `SIZE`, `MAXSIZE` e `FILEGROWTH` não podem ser definidos quando um caminho UNC está especificado para o arquivo.
>
> Bancos de dados do sistema não podem residir em diretórios de compartilhamento UNC.

Arquivos de dados não devem ser colocados em sistemas de arquivos compactados, a não ser que os arquivos sejam secundários e somente leitura ou que o banco de dados seja somente leitura. Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.

Se o arquivo estiver em uma partição bruta, *os_file_name* deverá especificar apenas a letra da unidade de uma partição bruta existente. Apenas um arquivo de dados pode ser colocado em cada partição bruta.

**'** *filestream_path* **'** Para um grupo de arquivos FILESTREAM, FILENAME faz referência a um caminho em que os dados FILESTREAM serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho `C:\MyFiles\MyFilestreamData`, `C:\MyFiles` deverá existir antes de você executar ALTER DATABASE, mas a pasta `MyFilestreamData` não deverá existir.

> [!NOTE]
> As propriedades SIZE e FILEGROWTH não se aplicam a um grupo de arquivos FILESTREAM.

**'** *memory_optimized_data_path* **'** Para um grupo de arquivos com otimização de memória, FILENAME refere-se a um caminho em que os dados com otimização de memória serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho `C:\MyFiles\MyData`, `C:\MyFiles` deverá existir antes de você executar ALTER DATABASE, mas a pasta `MyData` não deverá existir.

O grupo de arquivos e o arquivo (`<filespec>`) devem ser criados na mesma instrução.

> [!NOTE]
> As propriedades SIZE e FILEGROWTH não se aplicam a um grupo de arquivos MEMORY_OPTIMIZED_DATA.

Para obter mais informações sobre grupos de arquivos otimizados para memória, confira [O grupo de arquivos otimizados para memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).

SIZE *size* Especifica o tamanho do arquivo. SIZE não se aplica a grupos de arquivos FILESTREAM.

*size* É o tamanho do arquivo.

Quando especificado com ADD FILE, *size* é o tamanho inicial do arquivo. Quando especificado com MODIFY FILE, *size* é o novo tamanho do arquivo e deve ser maior que o tamanho do arquivo atual.

Quando o *tamanho* do arquivo primário não é informado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o tamanho do arquivo primário no **modelo** de banco de dados. Quando um arquivo de dados ou arquivo de log secundário for especificado, mas *size* não for, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] torna o arquivo em um arquivo de 1 MB.

Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Para especificar uma fração de um megabyte, converta o valor em kilobytes multiplicando o número por 1024. Por exemplo, especifique 1536 KB em vez de 1,5 MB (1,5 x 1024 = 1536).

> [!NOTE]
> `SIZE` não pode ser definido:
>
> - Quando um caminho UNC está especificado para o arquivo
> - Para grupos de arquivos `FILESTREAM` e `MEMORY_OPTIMIZED_DATA`

MAXSIZE { *max_size*| UNLIMITED } Especifica o tamanho de arquivo máximo até o qual o arquivo pode crescer.

*max_size* É o tamanho de arquivo máximo. Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Se *max_size* não for especificado, o tamanho do arquivo aumentará até que o disco fique cheio.

UNLIMITED Especifica que o arquivo crescerá até que o disco esteja cheio. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um arquivo de log especificado com crescimento ilimitado tem um tamanho máximo de 2 TB, e um arquivo de dados tem um tamanho máximo de 16 TB. Não há nenhum tamanho máximo quando essa opção é especificada para um contêiner FILESTREAM. Ele continua crescendo até que o disco esteja cheio.

> [!NOTE]
> `MAXSIZE` não pode ser definido quando um caminho UNC está especificado para o arquivo.

FILEGROWTH *growth_increment* Especifica o incremento de crescimento automático do arquivo. A configuração de FILEGROWTH de um arquivo não pode exceder a configuração de MAXSIZE. FILEGROWTH não se aplica a grupos de arquivos FILESTREAM.

*growth_increment* É a quantidade de espaço adicionada ao arquivo sempre que novo espaço é necessário.

O valor pode ser especificado em MB, KB, GB, TB ou porcentagem (%). Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB. Quando % está especificada, o tamanho do incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. O tamanho especificado é arredondado para o mais próximo de 64 KB.

Um valor 0 indica que o crescimento automático está definido como off e nenhum espaço adicional é permitido.

Se FILEGROWTH não é especificado, os valores padrão são:

|Versão|Valores padrão|
|-------------|--------------------|
|A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Dados 64 MB. Arquivos de log 64 MB.|
|A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 1 MB. Arquivos de log 10%.|
|Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados 10%. Arquivos de log 10%.|

> [!NOTE]
> `FILEGROWTH` não pode ser definido:
>
> - Quando um caminho UNC está especificado para o arquivo
> - Para grupos de arquivos `FILESTREAM` e `MEMORY_OPTIMIZED_DATA`

OFFLINE Define o arquivo como offline e torna todos os objetos no grupo de arquivos inacessíveis.

> [!CAUTION]
> Só use essa opção quando o arquivo estiver corrompido e puder ser restaurado. Um arquivo definido como OFFLINE só pode ser definido como online por meio da restauração do arquivo do backup. Para obter mais informações sobre como restaurar um único arquivo, consulte [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).
>
> As opções \<filespec> não estão disponíveis em um Banco de Dados Independente.

**\<add_or_modify_filegroups>::=**

Adiciona, modifica ou remove um grupo de arquivos do banco de dados.

ADD FILEGROUP *filegroup_name* Adiciona um grupo de arquivos no banco de dados.

CONTAINS FILESTREAM Especifica que o grupo de arquivos armazena BLOBs (objetos binários grandes) FILESTREAM no sistema de arquivos.

CONTAINS MEMORY_OPTIMIZED_DATA

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior)

Especifica que o grupo de arquivos armazena dados com otimização de memória no sistema de arquivos. Para obter mais informações, veja [OLTP In-Memory – Otimização In-Memory](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Apenas um grupo de arquivos `MEMORY_OPTIMIZED_DATA` é permitido por banco de dados. Para criar tabelas com otimização de memória, o grupo de arquivos não pode estar vazio. Deve haver pelo menos um arquivo. *filegroup_name* se refere a um caminho. O caminho até a última pasta deve existir e a última pasta não deve existir.

REMOVE FILEGROUP *filegroup_name* Remove um grupo de arquivos do banco de dados. O grupo de arquivos não pode ser removido, a menos que esteja vazio. Remova todos os arquivos do grupo de arquivos primeiro. Para obter mais informações, consulte "REMOVE FILE *logical_file_name*", anteriormente neste tópico.

> [!NOTE]
> A menos que o Coletor de Lixo de FILESTREAM tenha removido todos os arquivos de um contêiner FILESTREAM, haverá falha e um erro será retornado na operação `ALTER DATABASE REMOVE FILE` para remover um contêiner FILESTREAM. Veja a seção [Remover um contêiner FILESTREAM](#removing-a-filestream-container) mais adiante neste tópico.

MODIFY FILEGROUP *filegroup_name* { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } Modifica o grupo de arquivos definindo o status como READ_ONLY ou READ_WRITE, transformando o grupo de arquivos no grupo de arquivos padrão para o banco de dados ou alterando o nome do grupo de arquivos.

\<filegroup_updatability_option> Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.

DEFAULT Altera o grupo de arquivos do banco de dados padrão para *filegroup_name*. Apenas um grupo de arquivos no banco de dados pode ser o grupo de arquivos padrão. Para obter mais informações, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).

NAME = *new_filegroup_name* Altera o nome do grupo de arquivos para o *new_filegroup_name*.

AUTOGROW_SINGLE_FILE **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior)

Quando um arquivo no grupo de arquivos atinge o limite de aumento automático, apenas esse arquivo aumenta. Esse é o padrão.

AUTOGROW_ALL_FILES

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior)

Quando um arquivo no grupo de arquivos atingir o limite de crescimento automático, todos os arquivos no grupo de arquivos crescerão.

> [!NOTE]
> Este é o valor padrão de TempDB.

**\<filegroup_updatability_option>::=**

Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.

READ_ONLY | READONLY Especifica o grupo de arquivos é somente leitura. Não são permitidas atualizações nos objetos. O grupo de arquivos primário não pode ser somente leitura. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.

Como um banco de dados somente leitura não permite modificações de dados:

- A recuperação automática é ignorada na inicialização do sistema.
- Não é possível reduzir o banco de dados.
- Não ocorrem bloqueios em bancos de dados somente leitura. Isso pode acelerar o desempenho das consultas.

> [!NOTE]
> A palavra-chave `READONLY` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar `READONLY` em novos projetos de desenvolvimento e planeje modificar os aplicativos que utilizam `READONLY` atualmente. Use `READ_ONLY` em vez disso.

READ_WRITE | READWRITE Especifica o grupo é READ_WRITE. As atualizações são habilitadas para os objetos no grupo de arquivos. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.

> [!NOTE]
> A palavra-chave `READWRITE` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar `READWRITE` em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente usam `READWRITE` para usar `READ_WRITE` em seu lugar.
> [!TIP]
> O status dessas opções pode ser determinado examinando a coluna **is_read_only** na exibição do catálogo **sys.databases** ou a propriedade **Updateability** da função `DATABASEPROPERTYEX`.

## <a name="remarks"></a>Comentários

Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).

Não é possível adicionar ou remover um arquivo enquanto uma instrução `BACKUP` está em execução.

Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.

Começando pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o estado de um arquivo de banco de dados (por exemplo, online ou offline) é mantido independentemente do estado do banco de dados. Para obter mais informações, consulte [Estados de arquivo](../../relational-databases/databases/file-states.md).

- O estado dos arquivos dentro de um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online.
- Se um grupo de arquivos estiver offline, qualquer tentativa de acessá-lo por meio de uma instrução SQL falhará com erro. Quando você cria planos de consulta para instruções `SELECT`, o otimizador de consulta evita índices não clusterizados e exibições indexadas que residem em grupos de arquivos offline. Isso permite que essas instruções tenham êxito. Porém, se o grupo de arquivos offline contiver o heap ou índice clusterizado da tabela de destino, as instruções `SELECT` falharão. Além disso, qualquer instrução `INSERT`, `UPDATE` ou `DELETE` que modifica uma tabela com um índice em um grupo de arquivos offline falhará.

Os parâmetros SIZE, MAXSIZE e FILEGROWTH não podem ser definidos quando um caminho UNC está especificado para o arquivo.

Os parâmetros SIZE e FILEGROWTH não podem ser definidos para grupos de arquivos otimizados para memória.

A palavra-chave `READONLY` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar `READONLY` em novos projetos de desenvolvimento e planeje modificar os aplicativos que utilizam READONLY no momento. Use `READ_ONLY` em vez disso.

A palavra-chave `READWRITE` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar `READWRITE` em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente usam `READWRITE` para usar `READ_WRITE` em seu lugar.

## <a name="moving-files"></a>Movendo arquivos

Você pode mover dados do sistema ou definidos pelo usuário e arquivos de log especificando o novo local em FILENAME. Isso pode ser útil nos seguintes cenários:

- Recuperação de falha. Por exemplo, o banco de dados está em modo suspeito ou desligado por falha no hardware.
- Realocação planejada.
- Realocação para manutenção de disco programada.

Para obter mais informações, consulte [Mover arquivos de bancos de dados](../../relational-databases/databases/move-database-files.md).

## <a name="initializing-files"></a>Inicializando arquivos

Por padrão, arquivos de dados e de log são inicializados por meio do preenchimento com zeros quando você executa uma das seguintes operações:

- Criar um banco de dados.
- Adicionar arquivos a um banco de dados existente.
- Aumentar o tamanho de um arquivo existente.
- Restaurar um banco de dados ou grupo de arquivos.

Arquivos de dados podem ser inicializados instantaneamente. Isso permite uma execução rápida dessas operações de arquivo. Para obter mais informações, consulte [Inicialização de arquivos de bancos de dados](../../relational-databases/databases/database-instant-file-initialization.md).

## <a name="removing-a-filestream-container"></a><a name="removing-a-filestream-container"></a> Removendo um contêiner FILESTREAM

Embora o contêiner FILESTREAM possa ter sido esvaziado por meio da operação "DBCC SHRINKFILE", o banco de dados ainda pode precisar manter referências aos arquivos excluídos por várias razões de manutenção do sistema. [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) executará o Coletor de Lixo de FILESTREAM para remover esses arquivos quando for seguro fazê-lo. A menos que o Coletor de Lixo de FILESTREAM tenha removido todos os arquivos de um contêiner FILESTREAM, a operação ALTER DATABASE REMOVE FILE não poderá remover um contêiner FILESTREAM e um erro será retornado. O processo a seguir é recomendado para remover um contêiner FILESTREAM.

1. Execute [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) com a opção EMPTYFILE para mover o conteúdo ativo desse contêiner para outros contêineres.
2. Verifique se foram executados backups de log no modelo de recuperação FULL ou BULK_LOGGED.
3. Verifique se o trabalho do leitor de log de replicação foi executado, se pertinente.
4. Execute [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) para forçar o coletor de lixo a excluir os arquivos que não são mais necessários nesse contêiner.
5. Execute ALTER DATABASE com a opção REMOVE FILE para remover este contêiner.
6. Repita as etapas 2 a 4 uma vez para concluir a coleta de lixo.
7. Use ALTER Database...REMOVE FILE para remover este contêiner.

## <a name="examples"></a>Exemplos

### <a name="a-adding-a-file-to-a-database"></a>a. Adicionando um arquivo a um banco de dados

O exemplo a seguir adiciona um arquivo de dados de 5 MB ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = Test1dat2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. Adicionando um grupo de arquivos com dois arquivos a um banco de dados

O exemplo a seguir cria o grupo de arquivos `Test1FG1` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e adiciona dois arquivos de 5 MB ao grupo de arquivos.

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),  
(  
    NAME = test1dat4,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO
```

### <a name="c-adding-two-log-files-to-a-database"></a>C. Adicionando dois arquivos de log a um banco de dados

O exemplo a seguir adiciona dois arquivos de log de 5 MB ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD LOG FILE
(
    NAME = test1log2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1log3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="d-removing-a-file-from-a-database"></a>D. Removendo um arquivo de um banco de dados

O exemplo a seguir remove um dos arquivos adicionados no exemplo B.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="e-modifying-a-file"></a>E. Modificando um arquivo

O exemplo a seguir aumenta o tamanho de um dos arquivos adicionados no exemplo B. A instrução ALTER DATABASE com o comando MODIFY FILE só pode deixar um tamanho de arquivo maior, portanto, se você precisar diminuir o tamanho de arquivo, precisará usar DBCC SHRINKFILE.

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

Este exemplo reduz o tamanho de um arquivo de dados para 100 MB e, em seguida, especifica o tamanho nessa quantidade.

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="f-moving-a-file-to-a-new-location"></a>F. Movendo um arquivo para um novo local

O exemplo a seguir move o arquivo `Test1dat2` criado no exemplo A para um novo diretório.

> [!NOTE]
> Você deve mover o arquivo fisicamente para o novo diretório antes de executar este exemplo. Em seguida, interrompa e reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou coloque o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] OFFLINE e, em seguida, ONLINE para implementar a alteração.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(
    NAME = Test1dat2,
    FILENAME = N'c:\t1dat2.ndf'
);
GO
```

### <a name="g-moving-tempdb-to-a-new-location"></a>G. Movendo tempdb para um novo local

O exemplo a seguir move o `tempdb` de seu local atual no disco para outro local no disco. Como o `tempdb` é recriado cada vez que o serviço MSSQLSERVER é iniciado, não é necessário mover fisicamente os arquivos de dados e de log. Os arquivos são criados quando o serviço é reiniciado na etapa 3. Enquanto o serviço não é reiniciado, o `tempdb` continua funcionando em seu local existente.

1. Determine os nomes dos arquivos lógicos do banco de dados `tempdb` e o seu local atual no disco.

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    GO
    ```

2. Altere o local de cada arquivo usando `ALTER DATABASE`.

    ```sql
    USE master;
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');
    GO
    ```

3. Pare e reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

4. Verifique a alteração do arquivo.

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    ```

5. Exclua os arquivos tempdb.mdf e templog.ldf de seu local original.

### <a name="h-making-a-filegroup-the-default"></a>H. Tornando um grupo de arquivos o padrão

O exemplo a seguir torna o grupo de arquivos `Test1FG1` criado no exemplo B no grupo de arquivos padrão. Em seguida, o grupo de arquivos padrão é redefinido para o grupo de arquivos `PRIMARY`. Observe que `PRIMARY` deve ser delimitado por colchetes ou aspas.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="i-adding-a-filegroup-using-alter-database"></a>I. Adicionando um grupo de arquivos usando ALTER DATABASE

O exemplo a seguir adiciona um `FILEGROUP` que contém a cláusula `FILESTREAM` ao banco de dados `FileStreamPhotoDB`.

```sql
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause.
ALTER DATABASE FileStreamPhotoDB
ADD FILEGROUP TodaysPhotoShoot
CONTAINS FILESTREAM;
GO

--Add a file for storing database photos to FILEGROUP
ALTER DATABASE FileStreamPhotoDB
ADD FILE
(
  NAME= 'PhotoShoot1',
  FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'
)
TO FILEGROUP TodaysPhotoShoot;
GO
```

O exemplo a seguir adiciona um `FILEGROUP` que contém a cláusula `MEMORY_OPTIMIZED_DATA` ao banco de dados `xtp_db`. O grupo de arquivos armazena dados otimizados para memória.

```sql
--Create and add a FILEGROUP that CONTAINS the MEMORY_OPTIMIZED_DATA clause.
ALTER DATABASE xtp_db
ADD FILEGROUP xtp_fg
CONTAINS MEMORY_OPTIMIZED_DATA;
GO

--Add a file for storing memory optimized data to FILEGROUP
ALTER DATABASE xtp_db
ADD FILE
(
  NAME='xtp_mod',
  FILENAME='d:\data\xtp_mod'
)
TO FILEGROUP xtp_fg;
GO
```

### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. Alterar um grupo de arquivos para que, quando um arquivo no grupo de arquivos atinja o limite de aumento automático, todos os arquivos no grupo de arquivos aumentem

 O exemplo a seguir gera as instruções `ALTER DATABASE` necessárias para modificar grupos de arquivos de leitura/gravação com a configuração `AUTOGROW_ALL_FILES`.

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
  SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

  SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
  INSERT INTO #tmpfgs
  EXEC (@query)

  UPDATE #tmpdbs
  SET isdone = 1
  WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
  WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
  BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

    SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

    PRINT @query

    UPDATE #tmpfgs
    SET isdone = 1
    WHERE [dbid] = @dbid AND fgname = @fgname
  END
END;
GO
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [Objetos Binários Grandes](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)
- [DBCC SHRINKFIL](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
- [Inicialização de arquivo de bancos de dados](../../relational-databases/databases/database-instant-file-initialization.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql-file-and-filegroup-options.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* Instância gerenciada<br />do Banco de Dados SQL \*_**<br />&nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instância gerenciada do Banco de Dados SQL do Azure

Use esta instrução com um banco de dados na instância gerenciada do Banco de Dados SQL do Azure.

## <a name="syntax-for-databases-in-a-managed-instance"></a>Sintaxe para bancos de dados em uma instância gerenciada

```syntaxsql
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}
[;]

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}
  
<filespec>::=
(
    NAME = logical_file_name
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}  
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>Argumentos

**\<add_or_modify_files>::=**

Especifica o arquivo a ser adicionado, removido ou modificado.

*database_name* É o nome do banco de dados a ser modificado.

ADD FILE Adiciona um arquivo ao banco de dados.

TO FILEGROUP { *filegroup_name* } Especifica o grupo de arquivos ao qual adicionar o arquivo especificado. Para exibir os grupos de arquivos atuais e qual grupo de arquivos é o padrão atual, use a exibição do catálogo [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).

REMOVE FILE *logical_file_name* Remove a descrição do arquivo lógico de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui o arquivo físico. O arquivo não pode ser removido, a menos que esteja vazio.

*logical_file_name* É o nome lógico usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao fazer referência ao arquivo.

MODIFY FILE Especifica o arquivo que deve ser modificado. Apenas uma propriedade \<filespec> pode ser alterada por vez. NAME sempre deve ser especificado em \<filespec> para identificar o arquivo a ser modificado. Se SIZE for especificado, o novo tamanho deverá ser maior que o tamanho do arquivo atual.

**\<filespec>::=**

Controla as propriedades do arquivo.

NAME *logical_file_name* Especifica o nome lógico do arquivo.

*logical_file_name* É o nome lógico usado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao referenciar o arquivo.

NEWNAME *new_logical_file_name* Especifica um novo nome lógico para o arquivo.

*new_logical_file_name* É o nome para substituir o nome de arquivo lógico existente. O nome deve ser exclusivo dentro do banco de dados e obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md). O nome pode ser uma constante de caractere ou Unicode, um identificador comum ou delimitado.

SIZE *size* Especifica o tamanho do arquivo.

*size* É o tamanho do arquivo.

Quando especificado com ADD FILE, *size* é o tamanho inicial do arquivo. Quando especificado com MODIFY FILE, *size* é o novo tamanho do arquivo e deve ser maior que o tamanho do arquivo atual.

Quando o *tamanho* do arquivo primário não é informado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o tamanho do arquivo primário no **modelo** de banco de dados. Quando um arquivo de dados ou arquivo de log secundário for especificado, mas *size* não for, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] torna o arquivo em um arquivo de 1 MB.

Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Para especificar uma fração de um megabyte, converta o valor em kilobytes multiplicando o número por 1024. Por exemplo, especifique 1536 KB em vez de 1,5 MB (1,5 x 1024 = 1536).

MAXSIZE { *max_size*| UNLIMITED } Especifica o tamanho de arquivo máximo até o qual o arquivo pode crescer.

*max_size* É o tamanho de arquivo máximo. Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Se *max_size* não for especificado, o tamanho do arquivo aumentará até que o disco fique cheio.

UNLIMITED Especifica que o arquivo crescerá até que o disco esteja cheio. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um arquivo de log especificado com crescimento ilimitado tem um tamanho máximo de 2 TB, e um arquivo de dados tem um tamanho máximo de 16 TB.

FILEGROWTH *growth_increment* Especifica o incremento de crescimento automático do arquivo. A configuração de FILEGROWTH de um arquivo não pode exceder a configuração de MAXSIZE.

*growth_increment* É a quantidade de espaço adicionada ao arquivo sempre que novo espaço é necessário.

O valor pode ser especificado em MB, KB, GB, TB ou porcentagem (%). Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB. Quando % está especificada, o tamanho do incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. O tamanho especificado é arredondado para o mais próximo de 64 KB.

Um valor 0 indica que o crescimento automático está definido como off e nenhum espaço adicional é permitido.

Se FILEGROWTH não é especificado, os valores padrão são:

- Dados de 64 MB
- Arquivos de log de 64 MB

**\<add_or_modify_filegroups>::=**

Adiciona, modifica ou remove um grupo de arquivos do banco de dados.

ADD FILEGROUP *filegroup_name* Adiciona um grupo de arquivos no banco de dados.

O exemplo a seguir cria um grupo de arquivos que é adicionado a um banco de dados denominado sql_db_mi e adiciona um arquivo ao grupo de arquivos.

```sql
ALTER DATABASE sql_db_mi ADD FILEGROUP sql_db_mi_fg;
GO
ALTER DATABASE sql_db_mi ADD FILE (NAME='sql_db_mi_mod') TO FILEGROUP sql_db_mi_fg;
```

REMOVE FILEGROUP *filegroup_name* Remove um grupo de arquivos do banco de dados. O grupo de arquivos não pode ser removido, a menos que esteja vazio. Remova todos os arquivos do grupo de arquivos primeiro. Para obter mais informações, consulte "REMOVE FILE *logical_file_name*", anteriormente neste tópico.

MODIFY FILEGROUP _filegroup\_name_ { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } Modifica o grupo de arquivos definindo o status como READ_ONLY ou READ_WRITE, transformando o grupo de arquivos no grupo de arquivos padrão para o banco de dados ou alterando o nome do grupo de arquivos.

\<filegroup_updatability_option> Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.

DEFAULT Altera o grupo de arquivos do banco de dados padrão para *filegroup_name*. Apenas um grupo de arquivos no banco de dados pode ser o grupo de arquivos padrão. Para obter mais informações, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).

NAME = *new_filegroup_name* Altera o nome do grupo de arquivos para o *new_filegroup_name*.

AUTOGROW_SINGLE_FILE

Quando um arquivo no grupo de arquivos atinge o limite de aumento automático, apenas esse arquivo aumenta. Esse é o padrão.

AUTOGROW_ALL_FILES

Quando um arquivo no grupo de arquivos atingir o limite de crescimento automático, todos os arquivos no grupo de arquivos crescerão.

**\<filegroup_updatability_option>::=**

Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.

READ_ONLY | READONLY Especifica o grupo de arquivos é somente leitura. Não são permitidas atualizações nos objetos. O grupo de arquivos primário não pode ser somente leitura. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.

Como um banco de dados somente leitura não permite modificações de dados:

- A recuperação automática é ignorada na inicialização do sistema.
- Não é possível reduzir o banco de dados.
- Não ocorrem bloqueios em bancos de dados somente leitura. Isso pode acelerar o desempenho das consultas.

> [!NOTE]
> A palavra-chave READONLY será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar READONLY em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que o utilizam atualmente. Em vez disso, use READ_ONLY.

READ_WRITE | READWRITE Especifica o grupo é READ_WRITE. As atualizações são habilitadas para os objetos no grupo de arquivos. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.

> [!NOTE]
> A palavra-chave `READWRITE` será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar `READWRITE` em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente usam `READWRITE` para usar `READ_WRITE` em seu lugar.

O status dessas opções pode ser determinado examinando a coluna **is_read_only** na exibição do catálogo **sys.databases** ou a propriedade **Updateability** da função `DATABASEPROPERTYEX`.

## <a name="remarks"></a>Comentários

Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).

Não é possível adicionar ou remover um arquivo enquanto uma instrução `BACKUP` está em execução.

Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.

## <a name="examples"></a>Exemplos

### <a name="a-adding-a-file-to-a-database"></a>a. Adicionando um arquivo a um banco de dados

O exemplo a seguir adiciona um arquivo de dados de 5 MB ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
  NAME = Test1dat2,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. Adicionando um grupo de arquivos com dois arquivos a um banco de dados

O exemplo a seguir cria o grupo de arquivos `Test1FG1` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e adiciona dois arquivos de 5 MB ao grupo de arquivos.

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1dat4,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO

```

### <a name="c-removing-a-file-from-a-database"></a>C. Removendo um arquivo de um banco de dados

O exemplo a seguir remove um dos arquivos adicionados no exemplo B.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="d-modifying-a-file"></a>D. Modificando um arquivo

O exemplo a seguir aumenta o tamanho de um dos arquivos adicionados no exemplo B. A instrução ALTER DATABASE com o comando MODIFY FILE só pode deixar um tamanho de arquivo maior, portanto, se você precisar diminuir o tamanho de arquivo, precisará usar DBCC SHRINKFILE.

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

Este exemplo reduz o tamanho de um arquivo de dados para 100 MB e, em seguida, especifica o tamanho nessa quantidade.

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="e-making-a-filegroup-the-default"></a>E. Tornando um grupo de arquivos o padrão

O exemplo a seguir torna o grupo de arquivos `Test1FG1` criado no exemplo B no grupo de arquivos padrão. Em seguida, o grupo de arquivos padrão é redefinido para o grupo de arquivos `PRIMARY`. Observe que `PRIMARY` deve ser delimitado por colchetes ou aspas.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="f-adding-a-filegroup-using-alter-database"></a>F. Adicionando um grupo de arquivos usando ALTER DATABASE

O exemplo a seguir adiciona um `FILEGROUP` ao banco de dados `MyDB`.

```sql
--Create and add a FILEGROUP
ALTER DATABASE MyDB
ADD FILEGROUP NewFG;
GO

--Add a file to FILEGROUP
ALTER DATABASE MyDB
ADD FILE
(
    NAME= 'MyFile',
)
TO FILEGROUP NewFG;
GO
```

### <a name="g-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>G. Alterar um grupo de arquivos para que, quando um arquivo no grupo de arquivos atinja o limite de aumento automático, todos os arquivos no grupo de arquivos aumentem

O exemplo a seguir gera as instruções `ALTER DATABASE` necessárias para modificar grupos de arquivos de leitura/gravação com a configuração `AUTOGROW_ALL_FILES`.

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END;
GO
```

## <a name="see-also"></a>Consulte Também

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [O grupo de arquivos com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)

::: moniker-end
