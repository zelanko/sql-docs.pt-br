---
title: Compactação de dados | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- page compression [Database Engine]
- indexes [SQL Server], compressed
- compressed indexes [SQL Server]
- storage compression [Database Engine]
- tables [SQL Server], compressed
- storage [SQL Server], compressed
- compression [SQL Server]
- row compression [Database Engine]
- compression [SQL Server], about compressed tables and indexes
- data compression [Database Engine]
- compressed tables [SQL Server]
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bba6cc9159ac3cfc9cc45f882a916dcad3365e4e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533546"
---
# <a name="data-compression"></a>Data Compression
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] dão suporte à compactação de linhas e de páginas para tabelas e índices rowstore, e dão suporte a columnstore e à compactação de arquivamento columnstore para tabelas e índices columnstore.  
  
 Para tabelas e índices rowstore, use o recurso de compactação de dados para ajudar a reduzir o tamanho do banco de dados. Além de economizar espaço, a compactação de dados pode ajudar a aprimorar o desempenho de cargas de trabalho intensivas de E/S, pois os dados são armazenados em menos páginas e as consultas precisam ler menos páginas do disco. No entanto, recursos extras de CPU são necessários no servidor de banco de dados para compactar e descompactar os dados, enquanto os dados são trocados com o aplicativo. Você pode configurar a compactação de linha e página nos seguintes objetos de banco de dados:   
-   Uma tabela inteira que é armazenada como um heap.  
-   Uma tabela inteira que é armazenada como um índice clusterizado.  
-   Um índice não clusterizado inteiro.  
-   Uma exibição indexada inteira.  
-   Para tabelas e índices particionados, você pode configurar a opção de compactação para cada partição, e as várias partições de um objeto não precisam ter a mesma configuração de compactação.  
  
Para tabelas e índices columnstore, qualquer tabela e índice columnstore sempre usam a compactação columnstore, e isso não é configurável pelo usuário. Use a compactação de arquivamento columnstore para reduzir ainda mais o tamanho dos dados em situações em que tenha tempo extra e recursos de CPU para armazenar e recuperar os dados.  Você pode configurar a compactação de arquivamento columnstore nos seguintes objetos de banco de dados:  
-   Uma tabela columnstore inteira ou um índice columnstore clusterizado inteiro.  Desde que uma tabela columnstore é armazenada como um índice columnstore clusterizado, ambas as abordagens têm os mesmos resultados.  
-   Um índice columnstore não clusterizado inteiro.  
-   Para tabelas columnstore particionadas e índices columnstore, você pode configurar a opção de compactação de arquivamento para cada partição, e as várias partições não precisam ter a mesma configuração de compactação de arquivamento.  
  
> [!NOTE]  
>  Os dados também podem ser compactados usando o formato de algoritmo GZIP. Essa é uma etapa adicional e é mais adequada para compactar partes dos dados ao arquivar dados antigos para armazenamento de longo prazo. Os dados compactados usando a função COMPRESS não podem ser indexados. Para obter mais informações, veja [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md).  
  
## <a name="considerations-for-when-you-use-row-and-page-compression"></a>Considerações sobre quando usar a compactação de linha e de página  
 Ao usar compactação de linha e de página, esteja atento às seguintes considerações:  
-   Os detalhes de compactação de dados estão sujeitos a alteração sem aviso em service packs ou versões subsequentes.
-   A compactação está disponível em [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]  
-   A compactação não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
-   A compactação não está disponível para tabelas do sistema.  
-   A compactação pode permitir que mais linhas sejam armazenadas em uma página, mas não altera o tamanho máximo de linha de uma tabela ou de um índice.  
-   Uma tabela não pode ser habilitada para compactação quando o tamanho máximo da linha mais a sobrecarga de compactação exceder o tamanho máximo de linha de 8060 bytes. Por exemplo, uma tabela que tenha as colunas c1**char(8000)** e c2**char(53)** não pode ser compactada devido à sobrecarga de compactação adicional. Quando o formato de armazenamento vardecimal é usado, a verificação do tamanho da linha é executada quando o formato é habilitado. Para a compactação de linha e de página, a verificação do tamanho da linha é executada quando o objeto é inicialmente compactado e, depois, verificado à medida que cada linha é inserida ou modificada. A compactação impõe as duas regras seguintes:  
    -   Uma atualização para um tipo de comprimento fixo sempre deve ter êxito.  
    -   A desabilitação da compactação de dados sempre deve ter êxito. Mesmo que a linha compactada caiba em uma página, o que significa que ela é menor do que 8060 bytes, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impedirá atualizações que talvez não caibam na linha quando ela for descompactada.  
-   Quando uma lista de partições é especificada, o tipo de compactação deve ser definido como ROW, PAGE ou NONE em partições individuais. Se a lista de partições não for especificada, todas as partições serão definidas com a propriedade de compactação de dados especificada na instrução. Quando uma tabela ou índice é criado, a compactação dos dados é definida como NONE, a menos que especificada de outra maneira. Quando uma tabela é modificada a compactação existente é preservada, a menos que especificada de outra maneira.  
-   Se for especificada uma lista de partições ou uma partição fora do intervalo, um erro será gerado.  
-   Índices não clusterizados não herdam a propriedade de compactação da tabela. Para compactar índices, você deve definir explicitamente a propriedade de compactação dos índices. Por padrão, a configuração de compactação de índices é definida como NONE quando o índice é criado.  
-   Quando um índice clusterizado é criado em um heap, ele herda o estado de compactação do heap, a menos que um estado de compactação alternativo seja especificado.  
-   Quando um heap é configurado para compactação em nível de página, as páginas só recebem compactação em nível de página nos seguintes modos:  
    -   Os dados são importados em massa com otimizações em massa habilitadas.  
    -   Os dados são inseridos usando INSERT INTO ... A sintaxe WITH (TABLOCK) e a tabela não têm um índice não clusterizado.  
    -   Uma tabela é recriada executando ALTER TABLE ... Instrução REBUILD com a opção de compactação PAGE.  
-   As novas páginas alocadas em um heap como parte de operações DML não usam a compactação PAGE até o heap ser recompilado. Recompile o heap removendo e reaplicando a compactação ou criando e removendo um índice clusterizado.  
-   A alteração da configuração de compactação de um heap exige que todos os índices não clusterizados na tabela sejam recriados, para que tenham ponteiros para os novos locais de linha no heap.  
-   Você pode habilitar ou desabilitar a compactação de ROW ou PAGE online ou offline. A habilitação da compactação em um heap tem thread único para uma operação online.  
-   Os requisitos de espaço em disco para habilitar ou desabilitar a compactação de página ou de linha são os mesmos que para criar ou recriar um índice. Para dados particionados, você pode reduzir o espaço exigido para habilitar ou desabilitar a compactação para uma partição de cada vez.  
-   Para determinar o estado de compactação das partições em uma tabela particionada, consulte a coluna data_compression da exibição do catálogo sys.partitions.  
-   Quando você estiver compactando índices, as páginas de nível folha poderão ser compactadas com a compactação de linha e de página. As páginas que não são de nível folha não recebem a compactação de página.  
-   Devido ao seu tamanho, os tipos de dados de valor grande são, às vezes, armazenados separadamente dos dados de linhas normais em páginas com finalidades específicas. A compactação de dados não está disponível para os dados armazenados separadamente.  
-   As tabelas que implementaram o formato de armazenamento vardecimal no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] retêm essas configurações quando forem atualizadas. Você pode aplicar a compactação de linha a uma tabela com formato de armazenamento vardecimal. Entretanto, como a compactação de linha é um superconjunto de formato de armazenamento vardecimal, não há motivo para reter esse formato. Os valores decimais não ganham compactação adicional quando você combina o formato de armazenamento vardecimal com a compactação de linha. Só é possível aplicar a compactação de página a uma tabela com formato de armazenamento vardecimal; entretanto, as colunas de formato de armazenamento vardecimal provavelmente não alcançarão a compactação adicional.  
  
    > [!NOTE]  
    >  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte ao formato de armazenamento vardecimal; porém, como a compactação em nível de linha alcança as mesmas metas, o formato de armazenamento vardecimal é preterido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="using-columnstore-and-columnstore-archive-compression"></a>Usando a compactação columnstore e de arquivamento columnstore  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)].  
  
### <a name="basics"></a>Noções básicas  
 As tabelas e os índices columnstore são sempre armazenados com a compactação columnstore. Você pode reduzir ainda mais o tamanho dos dados de columnstore configurando um compactação adicional denominada compactação de arquivamento.  Para executar a compactação de arquivamento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa o algoritmo de compactação XPRESS da Microsoft nos dados. Adicione ou remova a compactação de arquivamento usando os seguintes tipos de compactação de dados:  
-   Use a compactação de dados **COLUMNSTORE_ARCHIVE** para compactar os dados de columnstore com a compactação de arquivamento.  
-   Use a compactação de dados **COLUMNSTORE** para descompactar a compactação de arquivamento. Esses dados resultantes continuam a ser compactados com a compactação columnstore.  
  
Para adicionar a compactação de arquivamento, use [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) com a opção REBUILD e DATA COMPRESSION = COLUMNSTORE_ARCHIVE.  
  
#### <a name="examples"></a>Exemplos:  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
```  
  
Para remover a compactação de arquivamento e restaurar os dados à compactação columnstoue, use [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) com a opção REBUILD e DATA COMPRESSION = COLUMNSTORE.  
  
#### <a name="examples"></a>Exemplos:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
```  
  
O exemplo a seguir define a compactação de dados para columnstore em algumas partições, e para o arquivamento columnstore em outras partições.  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### <a name="performance"></a>Desempenho  
 A compactação dos índices columnstore com a compactação de arquivamento faz com que o índice seja executado de forma mais lenta do que os índices columnstore que não têm a compactação de arquivamento. Use a compactação de arquivamento apenas quando tiver tempo extra e recursos de CPU para compactar e recuperar os dados.  
  
 O benefício da compactação de arquivamento é o armazenamento reduzido, que é útil para os dados que não são acessados com frequência. Por exemplo, se você tiver uma partição para cada mês de dados, e a maior parte da atividade for para os meses mais recentes, você poderá arquivar os meses anteriores para reduzir os requisitos de armazenamento.  
  
### <a name="metadata"></a>Metadados  
As seguintes exibições do sistema contêm informações sobre compactação de dados para índices clusterizados:  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) – As colunas **type** e **type_desc** incluem CLUSTERED COLUMNSTORE e NONCLUSTERED COLUMNSTORE.  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) – as colunas **data_compression** e **data_compression_desc** incluem COLUMNSTORE e COLUMNSTORE_ARCHIVE.  
  
O procedimento [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) não se aplica a índices columnstore.  
  
## <a name="how-compression-affects-partitioned-tables-and-indexes"></a>Como a compactação afeta tabelas e índices particionados  
 Ao usar a compactação de dados com tabelas e índices particionados, esteja atento às seguintes considerações:  
-   Quando as partições são divididas usando a instrução ALTER PARTITION, ambas as partições herdam o atributo de compactação de dados da partição original.  
-   Quando duas partições são mescladas, a partição resultante herda o atributo de compactação de dados da partição de destino.  
-   Para alternar uma partição, a propriedade de compactação de dados da partição deve corresponder à propriedade de compactação da tabela.  
-   Há duas variações de sintaxe que podem ser usadas para modificar a compactação de uma tabela ou índice particionado:  
    -   A sintaxe seguinte só recria a partição referenciada:  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
    -   A sintaxe seguinte recria a tabela inteira usando a configuração de compactação existente para qualquer partição não referenciada:  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     Os índices particionados seguem o mesmo princípio usando ALTER INDEX.  
  
-   Quando um índice clusterizado é descartado, as partições de heap correspondentes mantêm sua configuração de compactação de dados, a menos que o esquema de particionamento seja modificado. Se o esquema de particionamento for alterado, todas as partições serão recriadas para um estado não compactado. As etapas seguintes são necessárias para descartar um índice clusterizado e alterar o esquema de particionamento:  
     1. Descarte o índice clusterizado.  
     2. Modifique a tabela usando a opção ALTER TABLE ... REBUILD... que especifica a opção de compactação.  
  
     Descartar um índice clusterizado OFFLINE é uma operação rápida porque apenas os níveis superiores dos índices clusterizados são removidos. Quando um índice clusterizado é descartado ONLINE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve recriar o heap duas vezes, uma para a etapa 1 e outra para a etapa 2.  
  
## <a name="how-compression-affects-replication"></a>Como a compactação afeta a replicação 
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).   
Ao usar a compactação de dados com replicação, esteja atento às seguintes considerações:  
-   Quando o Agente de Instantâneo gera o script de esquema inicial, o novo esquema usa as mesmas configurações de compactação para a tabela e seus índices. A compactação não pode ser habilitada apenas na tabela e não no índice.  
-   Para replicação transacional, a opção de esquema de artigo determina quais objetos e propriedades dependentes devem ser incluídos no script. Para obter mais informações, veja [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
     O Agente de Distribuição não verifica Assinantes de nível inferior ao aplicar scripts. Se a replicação de compactação for selecionada, haverá falha na criação da tabela em Assinantes de nível inferior. Em caso de topologia mista, não habilite a replicação de compactação.  
-   Para replicação de mesclagem, o nível de compatibilidade da publicação substitui as opções de esquema e determina os objetos de esquema que são incluídos no script.  
     Em caso de topologia mista, se não for exigido o suporte a novas opções de compactação, o nível de compatibilidade da publicação deverá ser definido para a versão de Assinante de nível inferior. Se for exigido, será necessário compactar as tabelas no Assinante depois que elas forem criadas.  
  
A tabela a seguir mostra as configurações de replicação que controlam a compactação durante a replicação.  
  
|Intenção do usuário|Replicar esquema de partição para uma tabela ou um índice|Replicar configurações de compactação|Comportamento do script|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|Para replicar o esquema de partição e habilitar a compactação no Assinante da partição.|True|True|Gera scripts para o esquema da partição e as configurações de compactação.|  
|Para replicar o esquema da partição, mas não compactar os dados no Assinante.|True|Falso|Gera script para o esquema da partição, mas não para as configurações de compactação da partição.|  
|Para não replicar o esquema da partição e não compactar os dados no Assinante.|Falso|Falso|Não gera scripts para a partição nem para as configurações de compactação.|  
|Para compactar a tabela no Assinante, se todas as partições forem compactadas no Publicador, mas não replicar o esquema de partição.|Falso|True|Verifica se todas as partições estão habilitadas para compactação.<br /><br /> Gera scripts para a compactação em nível de tabela.|  
  
## <a name="how-compression-affects-other-sql-server-components"></a>Como a compactação afeta outros componentes do SQL Server 
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
   
 A compactação ocorre no mecanismo de armazenamento e os dados são apresentados à maioria dos outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um estado não compactado. Isso limita os efeitos da compactação nos outros componentes para:  
-   Operações de importação e exportação em massa  
     Quando os dados são exportados, mesmo em formato nativo, a saída dos dados é realizada no formato de linha descompactada. Isso pode fazer com que o tamanho do arquivo de dados exportado seja significativamente maior do que os dados de origem.  
     Quando os dados são importados, se a tabela de destino tiver sido habilitada para compactação, os dados serão convertidos pelo mecanismo de armazenamento em formato de linha compactada. Isso pode causar um aumento no uso da CPU se comparado à importação de dados em uma tabela descompactada.  
     Quando os dados são importados em massa para um heap com compactação de página, a operação de importação em massa tenta compactar os dados com a compactação de página quando eles forem inseridos.  
-   A compactação não afeta o backup e a restauração.  
-   A compactação não afeta o envio de logs.  
-   A compactação de dados é incompatível com colunas esparsas. Portanto, as tabelas que contêm colunas esparsas não podem ser compactadas, assim como as colunas esparsas não podem ser adicionadas a uma tabela compactada.  
-   A habilitação da compactação pode fazer com que os planos de consulta sejam alterados, porque os dados são armazenados usando um número diferente de páginas e um número de linhas por página.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementação da compactação de linha](../../relational-databases/data-compression/row-compression-implementation.md)   
 [Implementação da compactação de página](../../relational-databases/data-compression/page-compression-implementation.md)   
 [Implementação da compactação Unicode](../../relational-databases/data-compression/unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

