---
title: Arquivos e grupos de Arquivos de Banco de Dados | Microsoft Docs
ms.custom: 
ms.date: 10/11/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 73fde10c6cf318e5cd5c7eaa52a55a36f4d82001
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="database-files-and-filegroups"></a>Arquivos e grupos de arquivos do banco de dados
  Todo o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem, no mínimo, dois arquivos de sistema operacional: um arquivo de dados e um arquivo de log. Os arquivos de dados contêm dados e objetos como tabelas, índices, procedimentos armazenados e exibições. Os arquivos de log contêm as informações necessárias para recuperar todas as transações no banco de dados. Os arquivos de dados podem ser agrupados em grupos de arquivos para propósitos de alocação e administração.  
  
## <a name="database-files"></a>Arquivos do banco de dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possuem três tipos de arquivos, como mostrado na tabela a seguir.  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|Primária|O arquivo de dados primário contém as informações de inicialização do banco de dados e aponta para os outros arquivos no banco de dados. Dados do usuário e objetos podem ser armazenados neste arquivo ou em arquivos de dados secundários. Todo banco de dados possui um arquivo de dados primário. A extensão de nome de arquivo indicada para arquivos de dados primários é .mdf.|  
|Secundário|Os arquivos de dados secundários são opcionais, definidos pelo usuário, e armazenam dados do usuário. Arquivos secundários podem ser usados para distribuir os dados entre os diversos discos, colocando cada arquivo em uma unidade de disco diferente. Além disso, caso um banco de dados exceda o tamanho máximo em um único arquivo Windows, será possível usar arquivos de dados secundários, assim, o banco de dados continuará a crescer.<br /><br /> A extensão de nome de arquivo indicada para arquivos de dados secundários é .ndf.|  
|Log de Transações|Os arquivos de log de transações armazenam as informações de log usadas para recuperar o banco de dados. Deve haver, no mínimo, um arquivo de log para cada banco de dados. A extensão de nome de arquivo indicada para arquivos de transação é .ldf.|  
  
 Por exemplo, pode-se criar um simples banco de dados nomeado como **Vendas** que tenha um arquivo primário com todos os dados e objetos, e um arquivo de log que tenha as informações de log de transação. Como alternativa, pode-se criar um banco de dados mais complexo nomeado como **Pedidos** que tenha um arquivo primário e cinco arquivos secundários. Os dados e objetos no banco de dados distribuem-se pelos seis arquivos, e os quatro arquivos de log contêm as informações do log de transação.  
  
 Por padrão, os dados e logs de transação são colocados na mesma unidade e caminho. Isto é feito para controlar os sistemas de um único disco. Porém, isto não é o ideal para ambientes de produção. Recomendamos que você coloque os dados e arquivos de log em discos separados.  

### <a name="logical-and-physical-file-names"></a>Nomes de arquivos lógico e físico

Os arquivos do SQL Server têm dois nomes: 

**logical_file_name:**  O logical_file_name é o nome usado para se referir ao arquivo físico em todas as instruções Transact-SQL. O nome de arquivo lógico deve estar de acordo com as regras de identificadores do SQL Server e deve ser exclusivo entre os nomes de arquivos lógicos no banco de dados.

**os_file_name:** O os_file_name denomina é o nome do arquivo físico que inclui o caminho de diretório. Ele deve seguir as regras dos nomes de arquivo de sistema operacional.

Os arquivos de log e os dados do SQL Server podem ser colocados em sistemas de arquivos FAT ou NTFS. Recomendamos o uso do sistema de arquivos NTFS devido aos aspectos de segurança do NTFS. Os grupos de arquivos de dados de leitura/gravação e os arquivos de log não podem ser colocados em um sistema de arquivos compactados NTFS. Só podem ser colocados bancos de dados somente leitura e grupos de arquivos secundários somente leitura em um sistema de arquivos compactados NTFS.

Quando são executadas várias instâncias do SQL Server em um único computador, cada instância recebe um diretório padrão diferente para manter os arquivos dos bancos de dados criados na instância. Para obter mais informações, consulte [Locais de Arquivos para Instâncias Padrão e Nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).

### <a name="data-file-pages"></a>Páginas de arquivo de dados

As páginas de um arquivo de dados do SQL Server são numeradas em sequência, iniciando com zero (0) na primeira página do arquivo. Cada arquivo em um banco de dados tem um número de ID de arquivo exclusivo. Para identificar de forma exclusiva uma página em um banco de dados, são necessários ID do arquivo e número de página. O exemplo a seguir mostra os números de página em um banco de dados que tem um arquivo de dados primário de 4 MB e um arquivo de dados secundário de 1 MB.

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

A primeira página de cada arquivo é uma página de cabeçalho de arquivo que contém informações sobre os atributos do arquivo. Várias outras páginas do início do arquivo também têm informações de sistema, como mapas de alocação. Uma das páginas de sistema armazenada no arquivo de dados primário e no primeiro arquivo de log é uma página de inicialização de banco de dados que contém informações sobre os atributos do banco de dados. Para obter mais informações sobre essas páginas e os tipos de páginas, consulte Noções Básicas sobre Páginas e Extensões.

### <a name="file-size"></a>Tamanho do arquivo

Os arquivos do SQL Server podem aumentar automaticamente do tamanho original especificado. Ao definir um arquivo, você poderá definir um incremento de crescimento específico. Sempre que o arquivo estiver cheio, seu tamanho aumentará com base no incremento de crescimento. Se houver vários arquivos em um grupo de arquivos, eles não crescerão automaticamente até que todos os arquivos estejam cheios. O crescimento acontece na forma de rodízio.

Cada arquivo também pode ter um tamanho máximo especificado. Se um tamanho máximo não for especificado, o arquivo continuará crescendo até usar todo o espaço disponível no disco. Esse recurso é muito útil quando o SQL Server é usado como um banco de dados inserido em um aplicativo no qual o usuário não tem acesso conveniente a um administrador de sistema. O usuário pode deixar o crescimento automático de arquivos conforme exigido para reduzir a carga administrativa de monitoramento do espaço livre do banco de dados e de alocação manual de espaço adicional. 


## <a name="database-snapshot-files"></a>Arquivos de instantâneo do banco de dados

O formulário do arquivo usado por um instantâneo do banco de dados para armazenar seus dados de cópia-na-gravação depende de o instantâneo ser criado por um usuário ou usado internamente:

* Um instantâneo do banco de dados criado por um usuário armazena seus dados em um ou mais arquivos esparsos. A tecnologia de arquivo esparso é um recurso do sistema de arquivos NTFS. A princípio, um arquivo esparso não contém nenhum dado de usuário, e o espaço de disco para dados de usuário não foi alocado ao arquivo esparso. Para obter informações gerais sobre o uso de arquivos esparsos em instantâneos do banco de dados e como os instantâneos do banco de dados aumentam, consulte [Exibir o Tamanho do Arquivo Esparso do Instantâneo de Banco de Dados](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md). 
* Os instantâneos de banco de dados são usados internamente por determinados comandos DBCC. Esses comandos incluem DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC e DBCC CHECKFILEGROUP. Um instantâneo do banco de dados interno usa fluxos de dados alternativos esparsos dos arquivos de banco de dados originais. Assim como os arquivos esparsos, os fluxos de dados alternativos são um recurso do sistema de arquivos NTFS. O uso de fluxos de dados alternativos esparsos permite que as alocações de dados múltiplas sejam associadas a um único arquivo ou pasta sem afetar o tamanho do arquivo ou as estatísticas de volume. 


  
## <a name="filegroups"></a>Grupos de arquivos  
 Todo banco de dados possui um grupo de arquivo primário. Este grupo de arquivo contém o arquivo de dados primário e qualquer um dos arquivos secundários que não foram colocados em outros grupos de arquivos. Grupos de arquivos definidos pelo usuário podem ser criados para agrupar os arquivos de dados para fins administrativos, de alocação de dados e de posicionamento.  
  
 Por exemplo, três arquivos, Data1.ndf, Data2.ndf, e Data3.ndf, podem ser criados em três unidades de disco, respectivamente, e atribuídos ao grupo de arquivos **fgroup1**. Uma tabela pode ser criada especificamente no grupo de arquivos **fgroup1**. As consultas para obter dados da tabela serão distribuídas pelos três discos; isso melhorará o desempenho. A mesma melhora no desenvolvimento pode acontecer, usando um único arquivo criado em um conjunto distribuído RAID (redundant array of independent disks). Porém, arquivos e grupos de arquivos permitem que novos arquivos sejam facilmente adicionados aos novos discos.  
  
 Todos os arquivos de dados são armazenados nos grupos de arquivos listados na tabela a seguir.  
  
|Grupo de arquivos|Descrição|  
|---------------|-----------------|  
|Primária|O grupo de arquivos que contém o arquivo primário. Todas as tabelas do sistema são alocadas no grupo de arquivos primário.|  
|Definido pelo usuário|Qualquer grupo de arquivos que seja criado especificamente pelo usuário quando o usuário cria primeiro ou modifica depois o banco de dados.|  
  
### <a name="default-filegroup"></a>Grupo de arquivos padrão  
 Quando objetos são criados no banco de dados sem especificar a qual grupo de arquivos eles pertencem, os objetos são atribuídos ao grupo de arquivos padrão. A qualquer hora, um grupo de arquivos é designado como o grupo de arquivos padrão. Os arquivos no grupo de arquivos padrão devem ser grandes o suficientes para armazenar qualquer objeto novo alocado a outros grupos de arquivo.  
  
 O grupo de arquivos PRIMÁRIO é o grupo de arquivos padrão, a menos que seja alterado usando a instrução ALTER DATABASE. A alocação para os objetos de sistema e de tabelas permanece no grupo de arquivos PRIMÁRIO, e não no novo grupo de arquivos padrão.  

### <a name="file-and-filegroup-example"></a>Exemplo de arquivo e grupo de arquivos

O exemplo a seguir cria um banco de dados em uma instância do SQL Server. O banco de dados tem um arquivo de dados primário, um grupo de arquivos definido pelo usuário e um arquivo de log. O arquivo de dados primário está no grupo de arquivos primário e o grupo de arquivos definido pelo usuário tem dois arquivos de dados secundários. Uma instrução ALTER DATABASE torna padrão o grupo de arquivos definido pelo usuário. Depois, é criada uma tabela que especifica o grupo de arquivos definido pelo usuário. (Este exemplo usa um caminho genérico `c:\Program Files\Microsoft SQL Server\MSSQL.1` para evitar especificando uma versão do SQL Server.)

```
USE master;
GO
-- Create the database with the default data
-- filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB)
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO
```

A ilustração a seguir resume os resultados do exemplo anterior.

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
 [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
