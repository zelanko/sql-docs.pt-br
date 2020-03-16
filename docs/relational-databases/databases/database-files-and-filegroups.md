---
title: Arquivos e grupos de Arquivos de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 782536e79336c0224638707538e8a12a31f5af84
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287980"
---
# <a name="database-files-and-filegroups"></a>Arquivos e grupos de arquivos do banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
Os arquivos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm dois tipos de nome de arquivo: 

**logical_file_name:**  o logical_file_name é o nome usado para se referir ao arquivo físico em todas as instruções Transact-SQL. O nome de arquivo lógico deve estar de acordo com as regras de identificadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve ser exclusivo entre os nomes de arquivos lógicos no banco de dados. Isso é definido pelo argumento `NAME` em `ALTER DATABASE`. Para obter mais informações, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

**os_file_name:** o os_file_name é o nome do arquivo físico que inclui o caminho de diretório. Ele deve seguir as regras dos nomes de arquivo de sistema operacional. Isso é definido pelo argumento `FILENAME` em `ALTER DATABASE`. Para obter mais informações, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

> [!IMPORTANT]
> Os arquivos de log e os dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser colocados em sistemas de arquivos FAT ou NTFS. Em sistemas Windows, recomendamos o uso do sistema de arquivos NTFS devido aos aspectos de segurança do NTFS. 

> [!WARNING]
> Os grupos de arquivos de dados de leitura/gravação e os arquivos de log não são compatíveis com um sistema de arquivos compactados NTFS. Só podem ser colocados bancos de dados somente leitura e grupos de arquivos secundários somente leitura em um sistema de arquivos compactados NTFS.
> Para economia de espaço, é altamente recomendável usar a [compactação de dados](../../relational-databases/data-compression/data-compression.md) em vez da compactação do sistema de arquivos.

Quando várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executadas em um único computador, cada instância recebe um diretório padrão diferente para manter os arquivos dos bancos de dados criados na instância. Para obter mais informações, consulte [Locais de Arquivos para Instâncias Padrão e Nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).

### <a name="data-file-pages"></a>Páginas de arquivo de dados
As páginas de um arquivo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são numeradas em sequência, iniciando com zero (0) para a primeira página do arquivo. Cada arquivo em um banco de dados tem um número de ID de arquivo exclusivo. Para identificar de forma exclusiva uma página em um banco de dados, são necessários ID do arquivo e número de página. O exemplo a seguir mostra os números de página em um banco de dados que tem um arquivo de dados primário de 4 MB e um arquivo de dados secundário de 1 MB.

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

A primeira página de cada arquivo é uma página de cabeçalho de arquivo que contém informações sobre os atributos do arquivo. Várias outras páginas do início do arquivo também têm informações de sistema, como mapas de alocação. Uma das páginas de sistema armazenada no arquivo de dados primário e no primeiro arquivo de log é uma página de inicialização de banco de dados que contém informações sobre os atributos do banco de dados. Para obter mais informações sobre páginas e tipos de página, consulte o [Guia de arquitetura de páginas e extensões](../..//relational-databases/pages-and-extents-architecture-guide.md).

### <a name="file-size"></a>Tamanho do arquivo
Os arquivos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem aumentar automaticamente a partir do tamanho original especificado. Ao definir um arquivo, você poderá definir um incremento de crescimento específico. Sempre que o arquivo estiver cheio, seu tamanho aumentará com base no incremento de crescimento. Se houver vários arquivos em um grupo de arquivos, eles não crescerão automaticamente até que todos os arquivos estejam cheios. O aumento ocorre em um modo round robin usando o [preenchimento proporcional](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill).

Cada arquivo também pode ter um tamanho máximo especificado. Se um tamanho máximo não for especificado, o arquivo continuará crescendo até usar todo o espaço disponível no disco. Esse recurso é muito útil quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado como um banco de dados inserido em um aplicativo em que o usuário não tem acesso conveniente a um administrador de sistema. O usuário pode deixar o crescimento automático de arquivos conforme exigido para reduzir a carga administrativa de monitoramento do espaço livre do banco de dados e de alocação manual de espaço adicional.  

Se a [IFI (Inicialização Instantânea de Arquivo)](../../relational-databases/databases/database-instant-file-initialization.md) estiver habilitada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haverá uma sobrecarga mínima ao alocar um novo espaço a arquivos de dados.

Para obter mais informações sobre o gerenciamento de arquivos de log de transações, consulte [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations).   

## <a name="database-snapshot-files"></a>Arquivos de instantâneo do banco de dados
O formulário do arquivo usado por um instantâneo do banco de dados para armazenar seus dados de cópia-na-gravação depende de o instantâneo ser criado por um usuário ou usado internamente:

* Um instantâneo do banco de dados criado por um usuário armazena seus dados em um ou mais arquivos esparsos. A tecnologia de arquivo esparso é um recurso do sistema de arquivos NTFS. A princípio, um arquivo esparso não contém nenhum dado de usuário, e o espaço de disco para dados de usuário não foi alocado ao arquivo esparso. Para obter informações gerais sobre o uso de arquivos esparsos em instantâneos do banco de dados e como os instantâneos do banco de dados aumentam, consulte [Exibir o Tamanho do Arquivo Esparso do Instantâneo de Banco de Dados](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md). 
* Os instantâneos de banco de dados são usados internamente por determinados comandos DBCC. Esses comandos incluem DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC e DBCC CHECKFILEGROUP. Um instantâneo do banco de dados interno usa fluxos de dados alternativos esparsos dos arquivos de banco de dados originais. Assim como os arquivos esparsos, os fluxos de dados alternativos são um recurso do sistema de arquivos NTFS. O uso de fluxos de dados alternativos esparsos permite que as alocações de dados múltiplas sejam associadas a um único arquivo ou pasta sem afetar o tamanho do arquivo ou as estatísticas de volume. 
  
## <a name="filegroups"></a>Grupos de arquivos  
 Todo banco de dados possui um grupo de arquivo primário. Este grupo de arquivo contém o arquivo de dados primário e qualquer um dos arquivos secundários que não foram colocados em outros grupos de arquivos. Grupos de arquivos definidos pelo usuário podem ser criados para agrupar os arquivos de dados para fins administrativos, de alocação de dados e de posicionamento.  
  
 Por exemplo, três arquivos, `Data1.ndf`, `Data2.ndf` e `Data3.ndf`, podem ser criados em três unidades de disco, respectivamente, e atribuídos ao grupo de arquivos `fgroup1`. Uma tabela pode ser criada especificamente no grupo de arquivos `fgroup1`. As consultas para obter dados da tabela serão distribuídas pelos três discos; isso melhorará o desempenho. A mesma melhora no desenvolvimento pode acontecer, usando um único arquivo criado em um conjunto distribuído RAID (redundant array of independent disks). Porém, arquivos e grupos de arquivos permitem que novos arquivos sejam facilmente adicionados aos novos discos.  
  
 Todos os arquivos de dados são armazenados nos grupos de arquivos listados na tabela a seguir.  
  
|Grupo de arquivos|Descrição|  
|---------------|-----------------|  
|Primária|O grupo de arquivos que contém o arquivo primário. Todas as tabelas do sistema são alocadas no grupo de arquivos primário.|  
|Dados otimizados para memória|Um grupo de arquivos com otimização de memória baseia-se no grupo de arquivos do fluxo de arquivos|  
|Fluxo de arquivos||    
|Definido pelo usuário|Qualquer grupo de arquivos que seja criado especificamente pelo usuário quando o usuário cria primeiro ou modifica depois o banco de dados.|  
  
### <a name="default-primary-filegroup"></a>Grupo de arquivos padrão (primário)  
 Quando objetos são criados no banco de dados sem especificar a qual grupo de arquivos eles pertencem, os objetos são atribuídos ao grupo de arquivos padrão. A qualquer hora, um grupo de arquivos é designado como o grupo de arquivos padrão. Os arquivos no grupo de arquivos padrão devem ser grandes o suficientes para armazenar qualquer objeto novo alocado a outros grupos de arquivo.  
  
 O grupo de arquivos PRIMÁRIO é o grupo de arquivos padrão, a menos que seja alterado usando a instrução ALTER DATABASE. A alocação para os objetos de sistema e de tabelas permanece no grupo de arquivos PRIMÁRIO, e não no novo grupo de arquivos padrão.  
 
### <a name="memory-optimized-data-filegroup"></a>Grupo de arquivos de dados otimizado para memória

Para obter mais informações sobre grupos de arquivos com otimização de memória, consulte [Grupo de arquivos otimizado para memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).

### <a name="filestream-filegroup"></a>Grupos de arquivos de fluxo de arquivos

Para obter mais informações sobre grupos de arquivos de fluxo de arquivos, consulte [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md#filestream-storage) e [Criar um banco de dados habilitado para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).

### <a name="file-and-filegroup-example"></a>Exemplo de arquivo e grupo de arquivos
 O exemplo a seguir cria um banco de dados em uma instância do SQL Server. O banco de dados tem um arquivo de dados primário, um grupo de arquivos definido pelo usuário e um arquivo de log. O arquivo de dados primário está no grupo de arquivos primário e o grupo de arquivos definido pelo usuário tem dois arquivos de dados secundários. Uma instrução ALTER DATABASE torna padrão o grupo de arquivos definido pelo usuário. Depois, é criada uma tabela que especifica o grupo de arquivos definido pelo usuário. (Este exemplo usa um caminho genérico `c:\Program Files\Microsoft SQL Server\MSSQL.1` para evitar especificando uma versão do SQL Server.)

```sql
USE master;
GO
-- Create the database with the default data
-- filegroup, filstream filegroup and a log file. Specify the
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
    FILEGROWTH=1MB),
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM
  ( NAME = 'MyDB_FG_FS',
    FILENAME = 'c:\Data\filestream1')
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

-- Create a table in the filestream filegroup
CREATE TABLE MyFSTable
(
    cola int PRIMARY KEY,
  colb VARBINARY(MAX) FILESTREAM NULL
)
GO
```

A ilustração a seguir resume os resultados do exemplo anterior (exceto para os dados do fluxo de arquivos).

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)

## <a name="file-and-filegroup-fill-strategy"></a>Estratégia de arquivo e de preenchimento de grupo de arquivos
Os grupos de arquivos usam uma estratégia de preenchimento proporcional em todos os arquivos de cada grupo de arquivos. Como os dados são gravados no grupo de arquivos, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] grava uma quantidade proporcional no espaço livre de cada arquivo dentro do grupo de arquivos, em vez de gravar todos os dados no primeiro arquivo até que ele seja preenchido. Em seguida, grava no arquivo seguinte. Por exemplo, se o arquivo f1 tiver 100 MB livres e o arquivo f2 tiver 200 MB livres, uma extensão será alocada do arquivo f1, duas extensões do arquivo f2 e assim por diante. Dessa forma, todos os arquivos são preenchidos quase simultaneamente, e uma distribuição simples é obtida.

Tão logo todos os arquivos de um grupo de arquivos estejam preenchidos, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] expande automaticamente um arquivo por vez, de maneira sequencial, permitindo mais dados desde que o banco de dados esteja definido para aumentar de forma automática. Por exemplo, um grupo de arquivos compõe-se de três arquivos, todos definidos para aumentar automaticamente. Quando se extingue o espaço em todos os arquivos do grupo de arquivos, somente o primeiro arquivo é expandido. Quando o primeiro arquivo é preenchido e não é mais possível gravar dados no grupo de arquivos, o segundo arquivo é expandido. Quando o segundo arquivo está cheio e não é mais possível gravar dados no grupo de arquivos, o terceiro arquivo é expandido. Se o terceiro arquivos se tornar cheio e não for mais possível gravar dados no grupo de arquivos, o primeiro arquivo é expandido novamente, e assim por diante.

## <a name="rules-for-designing-files-and-filegroups"></a>Regras para criar arquivos e grupos de arquivos
As regras a seguir pertencem aos arquivos e grupos de arquivos:
- Arquivo ou grupos de arquivos não podem ser usados por mais que um banco de dados. Por exemplo, o arquivo sales.mdf e sales.ndf, que contêm dados e objetos do banco de dados sales, não podem ser usados por nenhum outro banco de dados.
- Um arquivo pode ser um membro apenas de um único grupo de arquivos.
- Os arquivos de log de transação nunca integram nenhum grupo de arquivos.

## <a name="Recommendations"></a> Recomendações
A seguir, algumas recomendações gerais para quando se estiver trabalhando com arquivos e grupos de arquivos: 
- A maioria dos bancos de dados funcionará bem com um único arquivo de dados e um único arquivo de log de transação.
- Se estiver usando vários arquivos de dados, crie um segundo grupo de arquivos para o arquivo adicional e transforme o grupo de arquivos no grupo de arquivos padrão. Desse modo, o arquivo primário conterá somente tabelas e objetos do sistema.
- Para maximizar o desempenho, crie arquivos ou grupos de arquivos no maior número possível de discos disponíveis diferentes. Insira objetos que disputem pesadamente por espaço em diferentes grupos de arquivos.
- Use grupos de arquivos para ativar a colocação de objetos em discos físicos específicos.
- Insira tabelas diferentes usadas nas mesmas consultas de junção em diferentes grupos de arquivos. Isto aperfeiçoará o desempenho por conta da busca por dados adicionados pela E/S paralela do disco.
- Insira tabelas excessivamente acessadas e índices não clusterizados que pertençam às tabelas de diferentes grupos de arquivos. Isto aperfeiçoará o desempenho por causa da E/S paralela caso os arquivos estejam localizados em discos físicos diferentes.
- Não insira os arquivos de log de transação no mesmo disco físico que contém os outros arquivos e grupos de arquivos.

Para obter mais informações sobre recomendações sobre o gerenciamento de arquivos de log de transações, consulte [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations).   

## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)    
 [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)      
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
 [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)    
 [Guia de arquitetura de página e extensões](../../relational-databases/pages-and-extents-architecture-guide.md)    
 [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)     
