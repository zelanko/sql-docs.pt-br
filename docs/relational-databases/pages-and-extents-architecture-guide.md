---
description: Guia de arquitetura de página e extensões
title: Guia de arquitetura de páginas e extensões | Microsoft Docs
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- page and extent architecture guide
- guide, page and extent architecture
ms.assetid: 83a4aa90-1c10-4de6-956b-7c3cd464c2d2
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dbee5b80fdb6f74ae3840f7728ae0eab2d24c28d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991847"
---
# <a name="pages-and-extents-architecture-guide"></a>Guia de arquitetura de página e extensões
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

A página é a unidade fundamental de armazenamento de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Uma extensão consiste em uma coleção de oito páginas fisicamente contíguas. As extensões ajudam a gerenciar páginas de maneira eficaz. Este guia descreve as estruturas de dados que são usadas para gerenciar páginas e extensões em todas as versões do SQL Server. Entender a arquitetura de páginas e extensões é importante para projetar e desenvolver bancos de dados que tenham um desempenho eficiente.

## <a name="pages-and-extents"></a>Páginas e Extensões

A unidade fundamental de armazenamento de dados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é a página. O espaço em disco alocado a um arquivo de dados (.mdf ou .ndf) em um banco de dados é logicamente dividido em páginas numeradas de forma contígua de 0 a n. As operações de E/S de disco são executadas no nível de página. Ou seja, o SQL Server lê ou grava páginas de dados inteiras.

As extensões são uma coleção de oito páginas fisicamente contíguas e são usadas para gerenciar as páginas de forma eficaz. Todas as páginas são organizadas em extensões.

### <a name="pages"></a>Pages (Páginas)

Pegue um livro regular: todo o conteúdo nele está escrito em páginas. Semelhante a um livro, no SQL Server, todas as linhas de dados são escritas em páginas. Em um livro, todas as páginas têm o mesmo tamanho físico. Da mesma forma, no SQL Server, todas as páginas de dados têm o mesmo tamanho – 8 quilobytes. Em um livro, a maioria das páginas contém os dados – o conteúdo principal do livro – e algumas páginas contêm metadados sobre o conteúdo – por exemplo, sumário e índice. Novamente, o SQL Server não é diferente: a maioria das páginas contém linhas reais de dados que foram armazenadas por usuários; elas são chamadas de Páginas de dados e páginas de texto/imagem (para casos especiais). As Páginas de índice contêm referências de índice sobre o local em que os dados estão e, finalmente, há páginas de sistema que armazenam uma variedade de metadados sobre a organização dos dados (páginas PFS, GAM, SGAM, IAM, DCM, BCM). Consulte a tabela abaixo para tipos de página e sua descrição.

Conforme mencionado, em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o tamanho da página é de 8 KB. Isso significa que os bancos de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] têm 128 páginas por megabyte. Cada página começa com um cabeçalho de 96 bytes usado para armazenar informações de sistema sobre a página. Essas informações incluem o número de página, o tipo de página, a quantidade de espaço livre na página e a ID de unidade de alocação do objeto que possui a página.

A tabela a seguir mostra os tipos de página usados nos arquivos de dados de um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

|Tipo de página | Conteúdo |
|-------|-------|
|Dados |Linhas de dados com todos os dados, exceto os dados de texto, ntext, imagem, nvarchar (max), varchar (max), varbinary (max) e xml, quando o texto na linha estiver definido como ON. |
|Índice |Entradas de índice. |
|Texto/Imagem |Tipos de dados de objeto grandes: (dados de texto, ntext, image, nvarchar(max), varchar(max), varbinary(max) e xml) <br> Colunas de comprimento variável quando a linha de dados exceder 8 KB: (varchar, nvarchar, varbinary e sql_variant) |
|Global Allocation Map, Shared Global Allocation Map |Informações sobre alocação de extensões. |
|PFS (Espaço Livre na Página) |Informações sobre alocação de página e espaço livre disponível em páginas. |
|Página IAM |Informações sobre extensões usadas por uma tabela ou índice por unidade de alocação. |
|Bulk Changed Map |Informações sobre extensões modificadas pelas operações em massa desde a última instrução BACKUP LOG por unidade de alocação. |
|Differential Changed Map |Informações sobre extensões modificadas desde a última instrução BACKUP DATABASE por unidade de alocação. |

> [!NOTE]
> Os arquivos de log não contêm páginas; eles contêm uma série de registros de log.

As linhas de dados são colocadas em série na página, iniciando imediatamente após o cabeçalho. Uma tabela de deslocamento da linha tem início no final da página, e cada tabela de deslocamento da linha contém uma entrada para cada linha na página. Cada entrada de deslocamento de linha registra a distância do primeiro byte da linha em relação ao início da página. Portanto, a função da tabela de deslocamento de linha é ajudar o SQL Server a localizar linhas em uma página muito rapidamente. As entradas na tabela de deslocamento da linha estão em sequência inversa da sequência das linhas na página.

![page_architecture](../relational-databases/media/page-architecture.gif)

#### <a name="large-row-support"></a>Suporte à linha grande  

As linhas não podem passar de uma página para outra, no entanto, partes da linha podem ser afastadas da página da linha para que a linha possa ser realmente muito grande. A quantidade máxima de dados e sobrecarga contida em uma única linha de uma página é de 8.060 bytes (8 KB). Porém, isso não inclui os dados armazenados no tipo de página de Texto/Imagem. 

Essa restrição é suavizada para tabelas que contêm colunas varchar, nvarchar, varbinary ou sql_variant. Quando o tamanho total da linha de todas as colunas fixas e variáveis em uma tabela exceder a limitação de 8.060 bytes, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] moverá uma ou mais colunas de comprimento variável dinamicamente para as páginas na unidade de alocação ROW_OVERFLOW_DATA, iniciando com a coluna com a maior largura. 

Isso é feito sempre que uma operação de inserção ou atualização aumenta o tamanho total da linha além do limite de 8.060 bytes. Quando uma coluna é movida para uma página na unidade de alocação ROW_OVERFLOW_DATA, é mantido um ponteiro de 24 bytes na página original da unidade de alocação IN_ROW_DATA. Se uma operação subsequente reduzir o tamanho da linha, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] moverá as colunas dinamicamente para a página de dados original. 

##### <a name="row-overflow-considerations"></a>Considerações sobre dados de estouro de linha 

Como mencionado anteriormente, uma linha não pode residir em várias páginas e poderá estourar se o tamanho combinado dos campos de tipo de dados de tamanho variável exceder o limite de 8.060 bytes. Para ilustrar isso, uma tabela pode ser criada com duas colunas: uma varchar(7000) e outra varchar(2000). Individualmente, nenhuma coluna excede os 8.060 bytes, mas, combinadas, elas poderão exceder esse limite caso a largura inteira de cada coluna seja preenchida. O SQL Server pode mover dinamicamente a coluna de tamanho variável varchar(7000) para as páginas na unidade de alocação ROW_OVERFLOW_DATA. Quando você combina colunas de tipo de dado CLR definido pelo usuário, varchar, nvarchar, varbinary ou sql_variant que excedem 8.060 bytes por linha, considere o seguinte:
-  A movimentação de registros volumosos para outra página ocorre dinamicamente à medida que os registros aumentam com base nas operações de atualização. As operações de atualização que diminuem os registros podem fazer com que os registros sejam retornados para a página original na unidade de alocação IN_ROW_DATA. A consulta e execução de outras operações de seleção, como classificações ou junções em grandes registros que contêm tempo de processamento de dados de estouro de linha lento, uma vez que esses registros são processados de forma síncrona em vez de assíncrona.   
   Portanto, quando você cria uma tabela com várias colunas de tipo de dado CLR definido pelo usuário, varchar, nvarchar, varbinary ou sql_variant, considere a porcentagem de linhas com probabilidade de exceder e a frequência com que os dados de estouro devem ser provavelmente consultados. Se houver provavelmente consultas frequentes em várias linhas dos dados de estouro de linha, considere normalizar a tabela de modo que algumas colunas sejam movidas para outra tabela. Em seguida, isso pode ser consultado em uma operação JOIN assíncrona. 
-  O comprimento de colunas individuais deve ainda se encaixar no limite de 8.000 bytes para colunas varchar, nvarchar, varbinary, sql_variant e colunas tipo de dado CLR definido pelo usuário. Só os comprimentos combinados delas podem exceder o limite de linha de 8.060 bytes de uma tabela.
-  A soma de outras colunas de tipo de dados, inclusive dados char e nchar deve enquadrar-se no limite de linha de 8.060 bytes. Dados de objeto grandes também estão isentos do limite de linha de 8.060 bytes. 
-  A chave de um índice clusterizado não pode conter colunas varchar que tenham dados existentes na unidade de alocação ROW_OVERFLOW_DATA. Se um índice clusterizado for criado em uma coluna varchar e os dados existentes estiverem na unidade de alocação IN_ROW_DATA, as ações subsequentes de inserção ou atualização na coluna que efetuaria o push dos dados da linha apresentarão falha. Para saber mais sobre unidades de alocação, veja Organização de tabela e índice.
-  Você pode incluir colunas contendo dados de estouro de linha como colunas de chave ou não chave de um índice não clusterizado.
-  O limite do tamanho de registros para tabelas que usam colunas esparsas é de 8.018 bytes. Quando os dados convertidos mais os dados de registros existentes ultrapassam os 8.018 bytes, é retornado o [ERRO MSSQLSERVER 576](../relational-databases/errors-events/database-engine-events-and-errors.md). Quando colunas são convertidas entre tipos esparsos e não esparsos, o Mecanismo de Banco de Dados mantém uma cópia dos dados de registros atuais. Isso dobra temporariamente o armazenamento exigido para o registro.
-  Para obter informações sobre tabelas ou índices que podem conter dados de estouro de linha, use a função de gerenciamento dinâmico [sys.dm_db_index_physical_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).

### <a name="extents"></a>Extensões 

As extensões são a unidade básica em que o espaço é gerenciado. Uma extensão tem oito páginas fisicamente contíguas ou 64 KB. Isso significa que os bancos de dados do SQL Server têm 16 extensões por megabyte.

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem dois tipos de extensões: 

* Extensões **uniformes** que pertencem a um único objeto; todas as oito páginas na extensão podem ser usadas apenas pelo objeto proprietário.
* Extensões **mistas** compartilhadas por até oito objetos. Cada uma das oito páginas da extensão pode pertencer a um objeto diferente.

![Extensões Uniformes e Mistas](../relational-databases/media/extents.gif)

Até, e incluindo, o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não aloca extensões inteiras a tabelas com quantidades pequenas de dados. Uma nova tabela ou índice geralmente aloca páginas de extensões mistas. Quando a tabela ou o índice cresce até adquirir oito páginas, é alternado para usar extensões uniformes para alocações subsequentes. Se um índice for criado em uma tabela existente que tiver linhas suficientes para gerar oito páginas no índice, todas as alocações para o índice estarão em extensões uniformes. 

A partir do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], o padrão para a maioria das alocações em um banco de dados de usuário e tempdb é usar extensões uniformes, exceto para alocações pertencentes às primeiras oito páginas de uma [cadeia de IAM](#IAM). As alocações para bancos de dados mestre, msdb e de modelo ainda mantêm o comportamento anterior. 

> [!NOTE]
> Até, e incluindo, o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], o sinalizador de rastreamento 1118 pode ser usado para alterar a alocação padrão para sempre usar extensões uniformes. Para obter mais informações sobre este sinalizador de rastreamento, consulte [DBCC TRACEON – Sinalizadores de rastreamento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   
>   
> A partir do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], a funcionalidade fornecida pelo FT 1118 é habilitada automaticamente para o tempdb. Para bancos de dados de usuário, esse comportamento é controlado pela opção `SET MIXED_PAGE_ALLOCATION` de `ALTER DATABASE`, com o valor padrão definido como OFF, e o sinalizador de rastreamento 1118 não tem nenhum efeito. Para obter mais informações, veja [Opções ALTER DATABASE SET (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-set-options.md).

A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], a função do sistema `sys.dm_db_database_page_allocations` pode relatar informações de alocação de página para um banco de dados, uma tabela, um índice e uma partição.

> [!IMPORTANT]
> A função do sistema `sys.dm_db_database_page_allocations` não está documentada e está sujeita a alterações. A compatibilidade não é garantida. 

A partir do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], a função do sistema [sys.dm_db_page_info](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) é disponibilizada e retorna informações sobre uma página em um banco de dados. A função retorna uma linha que contém as informações do cabeçalho da página, incluindo object_id, index_id e partition_id. Essa função substitui a necessidade de usar `DBCC PAGE` na maioria dos casos.

## <a name="managing-extent-allocations-and-free-space"></a>Gerenciando alocações de extensão e espaço livre 

As estruturas de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que gerenciam alocações de extensão e controlam o espaço livre têm uma estrutura relativamente simples. Ele oferece as seguintes vantagens: 

* As informações de espaço livre são compactadas, portanto, poucas páginas contêm essas informações.   
  Isso aumenta a velocidade reduzindo a quantidade de leituras de disco exigidas para recuperar as informações de alocação. Além disso, também aumenta a chance de as páginas de alocação permanecerem na memória e não exigirem mais leituras. 

* A maioria das informações de alocação não é encadeada. Isso simplifica a manutenção das informações de alocação.    
  Cada alocação ou desalocação de página pode ser executada rapidamente. O que diminui a contenção entre tarefas simultâneas que precisam alocar ou desalocar páginas. 

### <a name="managing-extent-allocations"></a>Gerenciando alocações de extensão

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa dois tipos de mapas de alocação para registrar a alocação de extensões: 

- **GAM (Global Allocation Map)**    
  As páginas GAM registram quais extensões foram alocadas. Cada GAM cobre 64.000 extensões ou quase 4 GB (gigabytes) de dados. O GAM tem 1 bit para cada extensão no intervalo que cobre. Se o bit for 1, a extensão será livre; se o bit for 0, a extensão será alocada. 

- **SGAM (Shared Global Allocation Map)**    
  As páginas SGAM registram quais extensões estão sendo usadas atualmente como extensões mistas e também têm pelo menos uma página não usada. Cada SGAM cobre 64.000 extensões ou quase 4 GB de dados. O GAM 1 um bit para cada extensão no intervalo que cobre. Se o bit for 1, a extensão será usada como uma extensão mista e terá uma página livre. Se o bit for 0, a extensão não será usada como uma extensão mista, ou será uma extensão mista e todas as suas páginas estarão sendo usadas. 

Cada extensão tem os padrões de bit a seguir configurados no GAM e no SGAM, com base em seu uso atual. 

|Uso atual da extensão | Configuração de bit GAM | Configuração de bit SGAM |
|---------|----------|------| 
|Livre, não está sendo usado |1 |0 |
|Extensão uniforme ou extensão mista completa |0 |0 |
|Extensão mista com páginas livres |0 |1 |
 
Isso gera algoritmos de gerenciamento de extensão simples. 
-   Para alocar uma extensão uniforme, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] pesquisa o GAM de um 1 bit e o define como 0. 
-   Para encontrar uma extensão mista com páginas livres, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] pesquisa o SGAM de um 1 bit. 
-   Para alocar uma extensão mista, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] pesquisa o GAM de um 1 bit, o define como 0 e define o bit correspondente no SGAM como 1. 
-   Para desalocar uma extensão, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] verifica se o bit do GAM está definido como 1 e o bit do SGAM como 0. Os algoritmos usados internamente pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] são mais complexos que os descritos neste artigo, porque o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] distribui dados uniformemente em um banco de dados. No entanto, até os algoritmos reais são simplificados por não precisarem gerenciar cadeias de informações de alocação de extensão.

### <a name="tracking-free-space"></a>Controlando o espaço livre

As páginas **PFS (Page Free Space)** registram o status de alocação de cada página, se uma página individual foi alocada e a quantidade de espaço livre em cada página. O PFS tem 1 byte para cada página, que registra se a página está alocada e, em caso afirmativo, se ela está vazia, de 1 a 50% completa, de 51 a 80% completa, de 81 a 95% completa ou de 96 a 100% completa.

Após a alocação de uma extensão a um objeto, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa as páginas PFS para registrar quais páginas na extensão são alocadas ou livres. Essas informações são usadas quando o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] precisa alocar uma página nova. A quantidade de espaço livre em uma página é mantida apenas para páginas heap e de Texto/Imagem. Ela é usada quando o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] precisa encontrar uma página com espaço livre disponível para manter uma linha recentemente inserida. Como o ponto em que a linha nova deve ser inserida é definido pelos valores de chave de índice, os índices não exigem que o espaço livre da página seja controlado.

Uma nova página PFS, GAM ou SGAM é adicionada ao arquivo de dados para cada intervalo adicional que ele acompanha. Portanto, há uma nova página PFS localizada a 8.088 páginas após a primeira página PFS e páginas PFS adicionais em intervalos de 8.088 páginas seguintes. Para ilustrar isso, a ID da página 1 é uma página PFS, a ID da página 8088 é uma página PFS, a ID da página 16176 é uma página PFS etc. Há uma nova página GAM localizada a 64.000 extensões após a primeira página GAM e ela acompanha os intervalos de 64.000 extensões posteriores; a sequência continua em intervalos de 64.000 extensões. Da mesma forma, há uma nova página SGAM localizada a 64.000 extensões após a primeira página SGAM e páginas SGAM adicionais nos intervalos de 64.000 extensões seguintes. A ilustração a seguir mostra a sequência de páginas usada pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] para alocar e gerenciar as extensões.

![manage_extents](../relational-databases/media/manage-extents.gif)

## <a name="managing-space-used-by-objects"></a><a name="IAM"></a> Como gerenciar o espaço usado por objetos 

Uma página **IAM** mapeia as extensões em uma parte de 4 GB de um arquivo de banco de dados usada por uma unidade de alocação. Uma unidade de alocação deve ser de um dos três tipos:

- IN_ROW_DATA   
    Mantém uma partição de um heap ou um índice.

- LOB_DATA   
   Contém tipos de dados de LOB (Objeto Grande), como VARCHAR(max), VARBINARY(max) e XML.

- ROW_OVERFLOW_DATA   
   Mantém dados de comprimento variáveis armazenados em colunas VARCHAR, NVARCHAR, VARBINARY OU SQL_VARIANT que excedem o limite de tamanho de linha de 8.060 bytes. 

Cada partição de um heap ou um índice contém pelo menos uma unidade de alocação de IN_ROW_DATA. Também pode conter uma unidade de alocação do LOB_DATA ou ROW_OVERFLOW_DATA, dependendo do esquema do heap ou índice.

Uma página IAM cobre um intervalo de 4 GB em um arquivo e tem a mesma cobertura de uma página GAM ou SGAM. Se a unidade de alocação contiver extensões de mais de um arquivo, ou mais de um intervalo de 4 GB de um arquivo, haverá várias páginas IAM vinculadas com uma cadeia de IAM. Portanto, cada unidade de alocação tem pelo menos uma página IAM para cada arquivo no qual tem extensões. Também poderá haver mais de uma página IAM em um arquivo, se o intervalo das extensões no arquivo alocado à unidade de alocação exceder o intervalo que uma única página IAM pode registrar. 

![iam_pages](../relational-databases/media/iam-pages.gif)

As páginas IAM são alocadas conforme exigido para cada unidade de alocação e ficam localizadas aleatoriamente no arquivo. A exibição do sistema `sys.system_internals_allocation_units` aponta para a primeira página de IAM de uma unidade de alocação. Todas as páginas de IAM dessa unidade de alocação são vinculadas em uma cadeia de IAM.

> [!IMPORTANT]
> A exibição de sistema `sys.system_internals_allocation_units` é destinada apenas para uso interno e está sujeita a alterações. A compatibilidade não é garantida. Esse modo de exibição não está disponível em [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. 

![iam_chain](../relational-databases/media/iam-chain.gif)
 
Páginas IAM vinculadas em uma unidade de cadeia por alocação. Uma página IAM tem um cabeçalho que indica a extensão inicial do intervalo de extensões mapeado pela página IAM. A página IAM também tem um bitmap grande no qual cada bit representa uma extensão. O primeiro bit no mapa representa a primeira extensão no intervalo, o segundo bit representa a segunda extensão, e assim por diante. Se um bit for 0, a extensão que ele representa não será alocada à unidade de alocação que possui IAM. Se o bit for 1, a extensão que ele representa será alocada à unidade de alocação que possui página IAM.

Quando o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] precisar inserir uma linha nova e não houver espaço disponível na página atual, ele usará as páginas IAM e PFS para localizar uma página para alocação ou, para um heap ou uma página de Texto/Imagem, uma página com espaço suficiente para manter a linha. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa as páginas IAM para localizar as extensões alocadas à unidade de alocação. Para cada extensão, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] pesquisa as páginas PFS para verificar se há uma página que possa ser usada. Cada página IAM e PFS abrange muitas páginas de dados, portanto, há poucas páginas IAM e PFS em um banco de dados. Isso significa que as páginas IAM e PFS geralmente estão na memória do pool de buffers [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], portanto, elas podem ser pesquisadas rapidamente. Para índices, o ponto de inserção de uma nova linha é definido pela chave de índice, mas quando uma nova página é necessária, ocorre o processo descrito anteriormente.

O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] só alocará uma extensão nova a uma unidade de alocação quando não conseguir encontrar uma página rapidamente em uma extensão existente com espaço suficiente para manter a linha que estiver sendo inserida. 

<a name="ProportionalFill"></a> O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] aloca as extensões disponíveis no grupo de arquivos usando um **algoritmo de alocação de preenchimento proporcional**. Se, em um grupo de arquivos com dois arquivos, um deles tiver duas vezes mais espaço livre do que o outro, serão alocadas duas páginas do arquivo com o espaço disponível para cada página alocada do outro arquivo. Isso significa que todo arquivo em um grupo de arquivos deve ter uma porcentagem semelhante de espaço usado. 

## <a name="tracking-modified-extents"></a>Controlando extensões modificadas 

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa duas estruturas de dados internas para acompanhar extensões modificadas por operações de cópia em massa e extensões modificadas desde o último backup completo. Essas estruturas de dados aceleram consideravelmente os backups diferenciais. Elas também aceleram o registro de operações de cópia em massa quando um banco de dados está usando o modelo de recuperação bulk logged. Como as páginas GAM (Global Alocação Map) e SGAM (Shared Global Allocation Map), essas estruturas são bitmaps em que cada bit representa uma única extensão. 

- **DCM (Differential Changed Map)**    
   Acompanha as extensões que foram alteradas desde a última instrução `BACKUP DATABASE`. Se o bit de uma extensão for 1, isso significa que a extensão foi modificada desde a última instrução `BACKUP DATABASE`. Se o bit for 0, a extensão não foi modificada. Os backups diferenciais leem apenas as páginas DCM para determinar quais extensões foram modificadas. Isso reduz significativamente o número de páginas que um backup diferencial deve examinar. O tempo de execução de um backup diferencial é proporcional ao número de extensões modificadas desde a última instrução BACKUP DATABASE, e não ao tamanho geral do banco de dados. 

- **BCM (Bulk Changed Map)**    
   Acompanha as extensões modificadas pelas operações registradas em log em massa desde a última instrução `BACKUP LOG`. Se o bit de uma extensão for 1, isso significará que a extensão foi modificada por uma operação registrada em log em massa após a última instrução `BACKUP LOG`. Se o bit for 0, a extensão não foi modificada pelas operações registradas em massa. Embora as páginas BCM sejam exibidas em todos os bancos de dados, elas serão relevantes apenas quando o banco de dados estiver usando o modelo de recuperação bulk-logged. Nesse modelo de recuperação, quando um `BACKUP LOG` é executado, o processo de backup examina os BCMs em busca das extensões que foram modificadas. Depois, inclui essas extensões no backup de log. Isso permite que as operações registradas em massa sejam recuperadas se o banco de dados for restaurado de um backup de banco de dados e uma sequência de backups de log de transações. As páginas BCM não são relevantes em um banco de dados que usa o modelo de recuperação simples, porque nenhuma operação registrada em massa está registrada. Elas não são relevantes em um banco de dados que usa o modelo de recuperação completo, porque o modelo de recuperação trata as operações com log em massa como operações registradas completas. 

O intervalo entre as páginas DCM e BCM é o mesmo que o intervalo entre as páginas GAM e SGAM, 64.000 extensões. As páginas DCM e BCM estão localizadas atrás das páginas GAM e SGAM em um arquivo físico:

![special_page_order](../relational-databases/media/special-page-order.gif)

## <a name="see-also"></a>Consulte Também
[sys.allocation_units &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
[Heaps &#40;Tabelas sem índices clusterizados&#41;](../relational-databases/indexes/heaps-tables-without-clustered-indexes.md#heap-structures)       
[sys.dm_db_page_info](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)     
[Lendo Páginas](../relational-databases/reading-pages.md)   
[Gravando Páginas](../relational-databases/writing-pages.md)   
