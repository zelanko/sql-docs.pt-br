---
title: "ALTERAR o arquivo de banco de dados e opções de grupo de arquivos (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 61
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fdd1f2aaab4e4aeeced6eb069255adba5b333abf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>Alterar opções de grupo de arquivos e arquivos de banco de dados (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica os arquivos e grupos de arquivos associados ao banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Adiciona ou remove arquivos e grupos de arquivos de um banco de dados e altera os atributos de um banco de dados ou seus arquivos e grupos de arquivos. Para obter outras opções de ALTER DATABASE, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
**\<add_or_modify_files >:: =**
  
 Especifica o arquivo a ser adicionado, removido ou modificado.  
  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
 ADD FILE  
 Adiciona um arquivo ao banco de dados.  
  
 Grupo de arquivos { *filegroup_name* }  
 Especifica o grupo de arquivos ao qual adicionar o arquivo especificado. Para exibir os grupos de arquivos atuais e o grupo de arquivos é o padrão atual, use o [sys. filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) exibição do catálogo.  
  
 ADD LOG FILE  
 Adiciona um arquivo de log ao banco de dados especificado.  
  
 REMOVER arquivo *logical_file_name*  
 Remove a descrição de arquivo lógico de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui o arquivo físico. O arquivo não pode ser removido, a menos que esteja vazio.  
  
 *logical_file_name*  
 É o nome lógico usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao referenciar o arquivo.  
  
> [!WARNING]  
>  Removendo um arquivo de banco de dados que tenha FILE_SNAPSHOT backups associados a ele terá êxito, mas não todos os instantâneos associados serão excluídos para evitar a anulação os backups que faz referência ao arquivo de banco de dados. O arquivo será truncado, mas não serão fisicamente excluído para manter os backups FILE_SNAPSHOT intactos. Para obter mais informações, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 MODIFY FILE  
 Especifica o arquivo que deve ser modificado. Apenas um \<filespec > propriedade pode ser alterada por vez. NOME sempre deve ser especificado no \<filespec > para identificar o arquivo a ser modificado. Se SIZE for especificado, o novo tamanho deverá ser maior que o tamanho do arquivo atual.  
  
 Para modificar o nome lógico de um arquivo de dados ou de um arquivo de log, especifique o nome do arquivo lógico a ser renomeado na cláusula `NAME` e especifique o novo nome lógico para o arquivo na cláusula `NEWNAME`. Por exemplo:  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 Para mover um arquivo de dados ou de log para um novo local, especifique o nome do arquivo lógico atual na cláusula `NAME` e especifique o novo caminho e o nome do arquivo do sistema operacional na cláusula `FILENAME`. Por exemplo:  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 Quando você move um catálogo de texto completo, especifique somente o novo caminho na cláusula FILENAME. Não especifique o nome do arquivo do sistema operacional.  
  
 Para obter mais informações, consulte [mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md).  
  
 Para um grupo de arquivos FILESTREAM, NAME pode ser modificado online. FILENAME pode ser modificado online; entretanto, a operação não entra em vigor até que o contêiner seja fisicamente realocado e o servidor seja desligado e reiniciado.  
  
 Você pode definir um arquivo FILESTREAM como OFFLINE. Quando um arquivo FILESTREAM estiver offline, seu grupo de arquivos pai será internamente marcado como offline; portanto, haverá falha em todo acesso aos dados FILESTREAM naquele grupo de arquivos.  
  
> [!NOTE]  
>  \<add_or_modify_files > Opções não estão disponíveis em um banco de dados independente.
  
 **\<filespec >:: =**  
  
 Controla as propriedades do arquivo.  
  
 NOME *logical_file_name*  
 Especifica o nome lógico do arquivo.  
  
 *logical_file_name*  
 É o nome lógico usado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao referenciar o arquivo.  
  
 NEWNAME *new_logical_file_name*  
 Especifica um novo nome lógico para o arquivo.  
  
 *new_logical_file_name*  
 É o nome para substituir o nome do arquivo lógico existente. O nome deve ser exclusivo no banco de dados e estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). O nome pode ser uma constante de caractere ou Unicode, um identificador comum ou delimitado.  
  
 Nome do arquivo { **'***os_file_name***'** | **'***filestream_path* **'** | **'***memory_optimized_data_path***'**}  
 Especifica o nome do arquivo (físico) do sistema operacional.  
  
 ' *os_file_name* '  
 Para um grupo de arquivos padrão (ROWS), esse é o caminho e o nome do arquivo usado pelo sistema operacional quando você cria o arquivo. O arquivo deve residir no servidor no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. O caminho especificado deve existir antes da execução da instrução ALTER DATABASE.  
  
 Os parâmetros SIZE, MAXSIZE e FILEGROWTH não podem ser definidos quando um caminho UNC está especificado para o arquivo.  
  
> [!NOTE]  
>  Bancos de dados do sistema não podem residir em diretórios de compartilhamento UNC.  
  
 Arquivos de dados não devem ser colocados em sistemas de arquivos compactados, a não ser que os arquivos sejam secundários e somente leitura ou que o banco de dados seja somente leitura. Arquivos de log nunca devem ser colocados em sistemas de arquivos compactados.  
  
 Se o arquivo estiver em uma partição bruta, *os_file_name* deve especificar somente a letra da unidade de uma partição bruta existente. Apenas um arquivo de dados pode ser colocado em cada partição bruta.  
  
 **'** *filestream_path* **'**  
 Para um grupo de arquivos FILESTREAM, FILENAME faz referência a um caminho onde dados FILESTREAM serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho C:\MyFiles\MyFilestreamData, C:\MyFiles deve existir antes da execução de ALTER DATABASE, mas a pasta MyFilestreamData não deve existir.  
  
 As propriedades SIZE e FILEGROWTH não se aplicam a um grupo de arquivos FILESTREAM.  
  
 **'** *memory_optimized_data_path* **'**  
 Para um grupo de arquivos com otimização de memória, FILENAME refere-se a um caminho em que os dados com otimização de memória serão armazenados. O caminho até a última pasta deve existir e a última pasta não deve existir. Por exemplo, se você especificar o caminho C:\MyFiles\MyData, C:\MyFiles deverá existir antes da execução de ALTER DATABASE, mas a pasta MyData não deverá existir.  
  
 O grupo de arquivos e o arquivo (`<filespec>`) devem ser criados na mesma instrução.  
  
 As propriedades SIZE, MAXSIZE e FILEGROWTH não se aplicam a um grupo de arquivos com otimização de memória.  
  
 TAMANHO *tamanho*  
 Especifica o tamanho do arquivo. SIZE não se aplica a grupos de arquivos FILESTREAM.  
  
 *tamanho*  
 É o tamanho do arquivo.  
  
 Quando especificado com ADD FILE *tamanho* é o tamanho inicial do arquivo. Quando especificado com MODIFY FILE *tamanho* é o novo tamanho para o arquivo e deve ser maior que o tamanho do arquivo atual.  
  
 Quando *tamanho* não for fornecido para o arquivo primário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o tamanho do arquivo primário no **modelo** banco de dados. Quando um arquivo de dados secundário ou um arquivo de log for especificado, mas *tamanho* não for especificado para o arquivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz com que o arquivo de 1 MB.  
  
 Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Para especificar uma fração de um megabyte, converta o valor em kilobytes multiplicando o número por 1024. Por exemplo, especifique 1536 KB em vez de 1,5 MB (1,5 x 1024 = 1536).  
  
 MAXSIZE { *max_size*| UNLIMITED}  
 Especifica o tamanho máximo do arquivo para o qual o arquivo pode crescer.  
  
 *max_size*  
 É o tamanho máximo do arquivo. Os sufixos KB, MB, GB e TB podem ser usados para especificar quilobytes, megabytes, gigabytes ou terabytes. O padrão é MB. Especifique um número inteiro e não inclua um decimal. Se *max_size* não for especificado, o tamanho do arquivo aumentará até que o disco está cheio.  
  
 UNLIMITED  
 Especifica que o arquivo crescerá até que o disco esteja cheio. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um arquivo de log especificado com crescimento ilimitado tem um tamanho máximo de 2 TB, e um arquivo de dados tem um tamanho máximo de 16 TB. Não há nenhum tamanho máximo quando essa opção é especificada para um contêiner FILESTREAM. Ele continua crescendo até que o disco esteja cheio.  
  
 FILEGROWTH *growth_increment*  
 Especifica o incremento de crescimento automático do arquivo. A configuração de FILEGROWTH de um arquivo não pode exceder a configuração de MAXSIZE. FILEGROWTH não se aplica a grupos de arquivos FILESTREAM.  
  
 *growth_increment*  
 É a quantidade de espaço adicionada ao arquivo sempre que novo espaço é necessário.  
  
 O valor pode ser especificado em MB, KB, GB, TB ou porcentagem (%). Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB. Quando % está especificada, o tamanho do incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. O tamanho especificado é arredondado para o mais próximo de 64 KB.  
  
 Um valor 0 indica que o crescimento automático está definido como off e nenhum espaço adicional é permitido.  
  
 Se FILEGROWTH não for especificado, os valores padrão são:  
  
|Versão|Valores padrão|  
|-------------|--------------------|  
|Início[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Dados de 64 MB. Os arquivos de log de 64 MB.|  
|Início[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados de 1 MB. Arquivos de log 10%.|  
|Antes de[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Dados de 10%. Arquivos de log 10%.|  
  
 OFFLINE  
 Define o arquivo como offline e torna todos os objetos no grupo de arquivos inacessíveis.  
  
> [!CAUTION]  
>  Só use essa opção quando o arquivo estiver corrompido e puder ser restaurado. Um arquivo definido como OFFLINE só pode ser definido como online por meio da restauração do arquivo do backup. Para obter mais informações sobre como restaurar um único arquivo, veja [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
> [!NOTE]  
>  \<espec de arquivo > Opções não estão disponíveis em um banco de dados independente.  
  
 **\<add_or_modify_filegroups >:: =**  
  
 Adiciona, modifica ou remove um grupo de arquivos do banco de dados.  
  
 Adicionar grupo de arquivos *filegroup_name*  
 Adiciona um grupo de arquivos ao banco de dados.  
  
 CONTAINS FILESTREAM  
 Especifica que o grupo de arquivos armazena BLOBs (objetos binários grandes) FILESTREAM no sistema de arquivos.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que o grupo de arquivos armazena dados com otimização de memória no sistema de arquivos. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Apenas um grupo de arquivos MEMORY_OPTIMIZED_DATA é permitido por banco de dados. Para criar tabelas com otimização de memória, o grupo de arquivos não pode estar vazio. Deve haver pelo menos um arquivo. *filegroup_name* se refere a um caminho. O caminho até a última pasta deve existir e a última pasta não deve existir.  
  
 O exemplo a seguir cria um grupo de arquivos que é adicionado a um banco de dados denominado xtp_db e adiciona um arquivo ao grupo de arquivos. O grupo de arquivos armazena dados memory_optimized.  
  
```  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 Remover grupo de arquivos *filegroup_name*  
 Remove um grupo de arquivos do banco de dados. O grupo de arquivos não pode ser removido, a menos que esteja vazio. Remova todos os arquivos do grupo de arquivos primeiro. Para obter mais informações, consulte "remover arquivo *logical_file_name*," anteriormente neste tópico.  
  
> [!NOTE]  
>  A menos que o Coletor de Lixo de FILESTREAM tenha removido todos os arquivos de um contêiner FILESTREAM, haverá falha e um erro será retornado na operação ALTER DATABASE REMOVE FILE para remover um contêiner FILESTREAM. Consulte a seção "Remover contêiner FILESTREAM" em Comentários posteriormente neste tópico.  
  
Modificar grupo de arquivos *filegroup_name* { \<filegroup_updatability_option > | PADRÃO | NOME  **=**  *new_filegroup_name* } modifica o grupo de arquivos, definindo o status como READ_ONLY ou READ_WRITE, tornando o grupo de arquivos padrão para o banco de dados, ou alterar o nome do grupo de arquivos.  
  
 \<filegroup_updatability_option >  
 Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.  
  
 DEFAULT  
 Altera o grupo de arquivos de banco de dados padrão para *filegroup_name*. Apenas um grupo de arquivos no banco de dados pode ser o grupo de arquivos padrão. Para obter mais informações, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 NOME = *new_filegroup_name*  
 Altera o nome do grupo de arquivos para o *new_filegroup_name*.  
  
 AUTOGROW_SINGLE_FILE  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Quando um arquivo no grupo de arquivos atingir o limite de crescimento automático, apenas aquele arquivo aumenta. Esse é o padrão.  
  
 AUTOGROW_ALL_FILES  

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Quando um arquivo no grupo de arquivos atingir o limite de crescimento automático, todos os arquivos no grupo de arquivos crescem.  
  
 **\<filegroup_updatability_option >:: =**  
  
 Define a propriedade somente leitura ou leitura/gravação para o grupo de arquivos.  
  
 READ_ONLY | READONLY  
 Especifica que o grupo de arquivos é somente leitura. Não são permitidas atualizações nos objetos. O grupo de arquivos primário não pode ser somente leitura. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.  
  
 Como um banco de dados somente leitura não permite modificações de dados:  
  
-   A recuperação automática é ignorada na inicialização do sistema.  
  
-   Não é possível reduzir o banco de dados.  
  
-   Não ocorrem bloqueios em bancos de dados somente leitura. Isso pode acelerar o desempenho das consultas.  
  
> [!NOTE]  
>  A palavra-chave READONLY será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar READONLY em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que o utilizam atualmente. Em vez disso, use READ_ONLY.  
  
 READ_WRITE | READWRITE  
 Especifica que o grupo é READ_WRITE. As atualizações são habilitadas para os objetos no grupo de arquivos. Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.  
  
> [!NOTE]  
>  A palavra-chave READWRITE será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar READWRITE em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que o utilizam atualmente. Em vez disso, use READ_WRITE.  
  
 O status dessas opções pode ser determinado examinando o **is_ready_only** coluna no **sys. Databases** exibição do catálogo ou o **Updateability** propriedade do Função DATABASEPROPERTYEX.  
  
## <a name="remarks"></a>Comentários  
 Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 Você não pode adicionar ou remover um arquivo enquanto uma instrução BACKUP está em execução.  
  
 Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, o estado de um arquivo de banco de dados (por exemplo, online ou offline) é mantido independentemente do estado do banco de dados. Para obter mais informações, consulte [estados de arquivo](../../relational-databases/databases/file-states.md). O estado dos arquivos dentro de um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Se um grupo de arquivos estiver offline, qualquer tentativa de acessá-lo por meio de uma instrução SQL falhará com erro. Quando você cria planos de consulta para instruções SELECT, o otimizador de consultas evita índices não clusterizados e exibições indexadas que residam em grupos de arquivos offline. Isso permite que essas instruções tenham êxito. Porém, se o grupo de arquivos offline contiver o heap ou índice clusterizado da tabela de destino, as instruções SELECT falharão. Além disso, qualquer instrução INSERT, UPDATE ou DELETE que modifique uma tabela contendo um índice em um grupo de arquivos offline falhará.  
  
## <a name="moving-files"></a>Movendo arquivos  
 Você pode mover dados do sistema ou definidos pelo usuário e arquivos de log especificando o novo local em FILENAME. Isso pode ser útil nos seguintes cenários:  
  
-   Recuperação de falha. Por exemplo, o banco de dados está em modo suspeito ou desligado devido a uma falha no hardware  
  
-   Realocação planejada  
  
-   Realocação para manutenção de disco programada  
  
 Para obter mais informações, consulte [mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md).  
  
## <a name="initializing-files"></a>Inicializando arquivos  
 Por padrão, arquivos de dados e de log são inicializados por meio do preenchimento com zeros quando você executa uma das seguintes operações:  
  
-   Criar um banco de dados  
  
-   Adicionar arquivos a um banco de dados existente  
  
-   Aumentar o tamanho de um arquivo existente  
  
-   Restaurar um banco de dados ou grupo de arquivos  
  
 Arquivos de dados podem ser inicializados instantaneamente. Isso permite uma execução rápida dessas operações de arquivo.  
  
## <a name="removing-a-filestream-container"></a>Removendo um contêiner FILESTREAM  
 Embora o contêiner FILESTREAM possa ter sido esvaziado por meio da operação "DBCC SHRINKFILE", o banco de dados ainda pode precisar manter referências aos arquivos excluídos por várias razões de manutenção do sistema. [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) executará o coletor de lixo de FILESTREAM para remover esses arquivos quando for seguro fazê-lo. A menos que o Coletor de Lixo de FILESTREAM tenha removido todos os arquivos de um contêiner FILESTREAM, a operação ALTER DATABASEREMOVE FILE não poderá remover um contêiner FILESTREAM e um erro será retornado. O processo a seguir é recomendado para remover um contêiner FILESTREAM.  
  
1.  Executar [DBCC SHRINKFILE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) com a opção EMPTYFILE para mover o conteúdo ativo desse contêiner para outros contêineres.  
  
2.  Verifique se foram executados backups de log no modelo de recuperação FULL ou BULK_LOGGED.  
  
3.  Verifique se o trabalho do leitor de log de replicação foi executado, se pertinente.  
  
4.  Executar [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) para forçar o coletor de lixo para excluir todos os arquivos que não são mais necessários neste contêiner.  
  
5.  Execute ALTER DATABASE com a opção REMOVE FILE para remover este contêiner.  
  
6.  Repita as etapas 2 a 4 uma vez para concluir a coleta de lixo.  
  
7.  Use ALTER Database...REMOVE FILE para remover este contêiner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-file-to-a-database"></a>A. Adicionando um arquivo a um banco de dados  
 O exemplo a seguir adiciona um arquivo de dados de 5 MB ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
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
  
```  
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
  
```  
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
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
  
```  
  
### <a name="e-modifying-a-file"></a>E. Modificando um arquivo  
O exemplo a seguir aumenta o tamanho de um dos arquivos adicionados no exemplo B.  
 A instrução ALTER DATABASE com o comando MODIFY FILE só pode tornar um tamanho de arquivo maior, então se você precisar reduzir o tamanho do arquivo, você precisa usar DBCC SHRINKFILE.  
  
```  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

Este exemplo reduz o tamanho de um arquivo de dados para 100 MB e, em seguida, especifica o tamanho em determinado período. 

```
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
>  Você deve mover o arquivo fisicamente para o novo diretório antes de executar este exemplo. Em seguida, interrompa e reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou coloque o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] OFFLINE e, em seguida, ONLINE para implementar a alteração.  
  
```  
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
  
1.  Determine os nomes dos arquivos lógicos do banco de dados `tempdb` e o seu local atual no disco.  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  Altere o local de cada arquivo usando `ALTER DATABASE`.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE  tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');  
    GO  
    ```  
  
3.  Pare e reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Verifique a alteração do arquivo.  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  Exclua os arquivos tempdb.mdf e templog.ldf de seu local original.  
  
### <a name="h-making-a-filegroup-the-default"></a>H. Tornando um grupo de arquivos o padrão  
 O exemplo a seguir torna o `Test1FG1` filegroup criado no exemplo B, o grupo de arquivos padrão. Em seguida, o grupo de arquivos padrão é redefinido para o grupo de arquivos `PRIMARY`. Observe que `PRIMARY` deve ser delimitado por colchetes ou aspas.  
  
```  
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
  
```  
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause to  
--the FileStreamPhotoDB database.  
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
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. Alterar o grupo de arquivos para que quando um arquivo no grupo de arquivos atingir o limite de crescimento automático, todos os arquivos no grupo de arquivos crescer
 O exemplo a seguir gera necessários `ALTER DATABASE` instruções para modificar grupos de arquivos de leitura / gravação com o `AUTOGROW_ALL_FILES` configuração.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys. filegroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
  
  

