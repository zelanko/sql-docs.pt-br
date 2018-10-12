---
title: Tabelas e índices particionados | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
- index partitions
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d421f828c93c932b4a554b80abcf94d2ca0ece6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734114"
---
# <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao particionamento de tabelas e índices. Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados. Os dados são particionados horizontalmente, de forma que os grupos de linhas são mapeados em partições individuais. Todas as partições de um único índice ou de uma única tabela devem residir no mesmo banco de dados. A tabela ou o índice é tratado como uma única entidade lógica quando são executadas consultas ou atualizações nos dados. Antes do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1, as tabelas e os índices particionados não estavam disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
> [!IMPORTANT]  
> O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte a até 15.000 partições por padrão. Em versões anteriores à [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o número de partições era limitado por padrão a 1.000. Em sistemas baseados em x86, é possível criar uma tabela ou índice com mais de 1.000 partições, mas isso não tem suporte.  
  
## <a name="benefits-of-partitioning"></a>Benefícios do particionamento  
 O particionamento de tabelas ou índices grandes pode ter a capacidade de gerenciamento e os benefícios de desempenho a seguir.  
  
-   Você pode transferir ou acessar subconjuntos de dados de forma rápida e eficaz e, ao mesmo tempo, manter a integridade de uma coleção de dados. Por exemplo, uma operação como o carregamento de dados de um sistema OLTP para OLAP leva apenas segundos, em vez dos minutos ou horas necessários quando os dados não estão paticionados.  
  
-   Você pode executar operações de manutenção mais rapidamente em uma ou mais partições. As operações são mais eficientes porque elas visam apenas estes subconjuntos de dados, e não a tabela inteira. Por exemplo, você pode optar por compactar dados em uma ou mais partições ou recriar uma ou mais partições de um índice.  
  
-   Você pode aprimorar o desempenho de consultas com base nos tipos de consultas executadas com frequência e em sua configuração de hardware. Por exemplo, o otimizador de consulta pode processar consultas de junção de igualdade entre duas ou mais tabelas particionadas mais rápido quando as colunas de particionamento nas tabelas são iguais, porque as próprias partições podem ser unidas.  
  
Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa classificação de dados para operações de E/S, ele classifica os dados primeiro pela partição. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acessa uma unidade de cada vez e isso pode reduzir o desempenho. Para melhorar o desempenho da classificação de dados, distribua os arquivos de dados de suas partições em mais de um disco configurando um RAID. Dessa maneira, embora o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda classifique os dados por partição, ele pode acessar todas as unidades de cada partição ao mesmo tempo.  
  
Além disso, você pode melhorar o desempenho habilitando o escalonamento de bloqueios em nível de partição em, e não em uma tabela inteira. Isso pode reduzir a contenção de bloqueio na tabela. Para reduzir a contenção de bloqueio permitindo o escalonamento de bloqueios para a partição, defina opção `LOCK_ESCALATION` da instrução `ALTER TABLE` como AUTO. 
  
## <a name="components-and-concepts"></a>Componentes e conceitos  
As condições a seguir são aplicáveis ao particionamento de tabela e de índice.  
  
### <a name="partition-function"></a>Função de partição  
Um objeto de banco de dados que define como as linhas de uma tabela ou índice são mapeadas para um conjunto de partições, com base nos valores de determinada coluna, chamada de coluna de particionamento. Ou seja, a função de partição define o número de partições que a tabela terá e como serão definidos os limites das partições. Por exemplo, considerando uma tabela que contém dados de ordem de venda, você pode desejar particionar a tabela em doze (mensalmente) partições com base em uma coluna **datetime** como uma data de vendas.  
  
### <a name="partition-scheme"></a>Esquema de partição 
Um objeto de banco de dados que mapeia as partições de uma função de partição para um conjunto de grupos de arquivos. O principal motivo para colocar suas partições em grupos de arquivos separados é para garantir que poderá efetuar operações de backup em partições de forma independente. Isso porque se pode executar backups em grupos de arquivos individuais.  
  
### <a name="partitioning-column"></a>Coluna de particionamento  
A coluna de uma tabela ou índice que uma função de partição usa para particionar a tabela ou índice. Colunas computadas que participam de uma função de partição devem ser marcadas explicitamente como PERSISTED. Todos os tipos de dados que são válidos para uso como colunas de índice podem ser usados como uma coluna de particionamento, exceto **timestamp**. Os tipos de dados **ntext**, **text**, **image**, **xml**, **varchar(max)**, **nvarchar(max)** ou **varbinary(max)** não podem ser especificados. Também, não podem ser especificados o tipo definido pelo usuário do CLR (Common Language Runtime) do Microsoft .NET Framework e colunas de tipo de dados do alias.  
  
### <a name="aligned-index"></a>Índice alinhado  
Um índice que é baseado no mesmo esquema de partição que sua tabela correspondente. Quando uma tabela e seus índices estão em alinhamento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode trocar as partições rápida e eficientemente enquanto, mantém a estrutura de partição em ambos, tabela e seus índices. Um índice não precisa participar na mesma função de partição nomeada para ser alinhado com sua tabela base. No entanto, a função de partição do índice e a tabela base devem ser essencialmente o mesmo, no sentido em que:
 1. os argumentos das funções de partição têm o mesmo tipo de dados.
 2. elas definem o mesmo número de partições.
 3. elas definem os mesmos valores de limite para partições.  

#### <a name="partitioning-clustered-indexes"></a>Particionando índices clusterizados
Ao particionar um índice clusterizado, a chave de clustering deve conter a coluna de particionamento. Quando particiona um índice clusterizado não exclusivo e a coluna de particionamento não está explicitamente especificada na chave de clustering, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adiciona a coluna de particionamento, por padrão, à lista de chaves de índices clusterizados. Se o índice clusterizado for exclusivo, você deve especificar explicitamente que a chave de índice clusterizado contém a coluna de particionamento.        

#### <a name="partitioning-nonclustered-indexes"></a>Particionando índices não clusterizados
Ao particionar um índice não clusterizado exclusivo, a chave de índice deve conter a coluna de particionamento. Ao particionar um índice não clusterizado e não exclusivo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adiciona a coluna de particionamento, por padrão, como a coluna do índice não chave (incluída) para garantir que o índice estará alinhado com a tabela base. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não adicionará a coluna de particionamento ao índice se este já estiver presente no índice. 

### <a name="non-aligned-index"></a>Índice não alinhado  
Um índice particionado independentemente de sua tabela correspondente. Quer dizer, o índice tem um esquema de partição diferente ou é colocado em um grupo de arquivos separado da tabela base. A criação de um índice particionado não alinhado pode ser útil nos seguintes casos:  
-   A tabela base não foi particionada.  
-   A chave de índice é exclusiva e não contém a coluna de particionamento da tabela.  
-   Você deseja que a tabela base participe de junções colocadas com mais tabelas que usam colunas de junção diferentes.  

### <a name="partition-elimination"></a>Eliminação de partição
O processo pelo qual o otimizador de consulta acessa apenas as partições relevantes para satisfazer os critérios de filtro da consulta.  

## <a name="performance-guidelines"></a>Diretrizes de desempenho  
 O limite novo, superior de 15.000 partições afeta a memória, operações de índice particionadas, comandos DBCC e consultas. Esta seção descreve as implicações de desempenho de aumentar o número de partições acima de 1.000 e fornece soluções alternativas quando necessário. Com o limite no número máximo de partições elevado para 15.000, você pode armazenar dados por mais tempo. Porém, você só deve reter dados enquanto necessário e manter um equilíbrio entre desempenho e número de partições.  
  
### <a name="processor-cores-and-number-of-partitions-guidelines"></a>Diretrizes de núcleos de processador e número de partições  
 Para maximizar o desempenho com operações paralelas, é recomendado usar o mesmo número de partições que de núcleos de processador, até no máximo 64 (que é o número máximo de processadores paralelos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode utilizar).  
  
### <a name="memory-usage-and-guidelines"></a>Uso de memória e diretrizes  
 É recomendável usar pelo menos 16 GB de RAM se um número grande de partições estiver em uso. Se o sistema não tiver memória suficiente, instruções DML (linguagem de manipulação de dados), instruções DDL (linguagem de definição de dados) e outras operações poderão falhar devido à memória insuficiente. Sistemas com 16 GB de RAM que executam muitos processos com uso intenso de memória podem ficar sem memória em operações executadas em um número grande de partições. Portanto, quanto mais memória você tiver acima de 16 GB, menor será a probabilidade de encontrar problemas de desempenho e memória.  
  
 As limitações de memória podem afetar o desempenho ou habilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para construir um índice particionado. Este será o caso especialmente quando o índice não está alinhado com sua tabela base ou não está alinhado com o índice clusterizado, se a tabela já tiver um índice clusterizado aplicado a ela. Nesse caso, pode ser útil aumentar Opção de Configuração do Servidor index create memory. Para obter mais informações, consulte [Configurar a opção index create memory de configuração de servidor](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). 
  
### <a name="partitioned-index-operations"></a>Operações de índice particionado  
É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações.  
  
A criação e a recompilação de índices alinhados poderão demorar mais para serem executadas à medida que aumentar o número de partições. É recomendável não executar vários comandos de índice de criação e recriação ao mesmo tempo porque você pode encontrar problemas de desempenho e memória.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar uma classificação para construir índices particionados, ele construirá primeiro uma tabela de classificação para cada partição. Ele construirá as tabelas de classificação no respectivo grupo de arquivos de cada partição ou no **tempdb**, se a opção de índice SORT_IN_TEMPDB for especificada. Cada tabela de classificação exige uma quantia mínima de memória para construir. Quando você estiver construindo um índice particionado que está alinhado com a tabela base, uma tabela de classificação por vez será criada, usando menos memória. Porém, quando você estiver construindo um índice particionado não alinhado, as tabelas de classificação serão criadas ao mesmo tempo. Como resultado, deve haver memória suficiente para controlar essas classificações simultâneas. Quanto maior o número de partições, mais memória será necessária. O tamanho mínimo para cada tabela de classificação, para cada partição é de 40 páginas, com 8 quilobites por página. Por exemplo, um índice particionado não alinhado com 100 partições requer memória suficiente para classificar serialmente 4.000 (40 x 100) páginas ao mesmo tempo. Se essa memória estiver disponível, a operação de construção terá sucesso, mas o desempenho poderá ser afetado. Se essa memória não estiver disponível, a operação de criação falhará. Como alternativa, um índice particionado alinhado com 100 partições requer apenas memória suficiente para classificar serialmente 40 páginas, porque as classificações não são executadas ao mesmo tempo.  
  
 Para ambos os índices, alinhados e não alinhados, os requisitos de memória poderão ser maiores se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicar graus de paralelismo à operação de compilação em um computador multiprocessador. Isso ocorre porque quanto maior os graus de paralelismo, maior será o requisito de memória. Por exemplo, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define os graus de paralelismo como 4, um índice particionado não alinhado com 100 partições requer memória suficiente para quatro processadores para classificar serialmente 4.000 páginas, ao mesmo tempo, ou 16.000 páginas. Se o índice particionado for alinhado, o requisito de memória será reduzido para quatro processadores classificando 40 páginas, 160 (4 x 40) páginas. Você pode usar a opção de índice MAXDOP para reduzir os graus de paralelismo manualmente.  

### <a name="dbcc-commands"></a>Comandos DBCC  
Com um número maior de partições, os comandos DBCC podem demorar mais para serem executados à medida que aumentar o número de partições.  
  
### <a name="queries"></a>Consultas  
Consultas que usam a eliminação de partição podem ter desempenho comparável ou aprimorado com número maior de partições. Consultas que não usam a eliminação de partição podem levar mais tempo para executar à medida que o número de partições aumenta.  
  
Por exemplo, digamos que uma tabela tem 100 milhões de linhas e colunas `A`, `B`e `C`. 
-  No cenário 1, a tabela é dividida em 1.000 partições na coluna `A`. 
-  No cenário 2, a tabela é dividida em 10.000 partições na coluna `A`. Uma consulta na tabela que tem uma cláusula `WHERE` filtrada na coluna `A` executará a eliminação de partição e examinará uma partição. Essa mesma consulta pode ser executada mais rapidamente no cenário 2, pois há menos linhas a serem examinadas em uma partição. Uma consulta com uma cláusula `WHERE` filtrada na coluna B examinará todas as partições. A consulta pode ser executada mais rapidamente no cenário 1 do que no cenário 2, pois há menos partições a serem examinadas.  

As consultas que usam operadores como TOP ou MAX/MIN em colunas que não sejam a coluna de particionamento podem sofrer redução do desempenho com o particionamento porque todas as partições precisam ser avaliadas.  

Se você executar consultas que envolvem uma junção de igualdade (equi-join) entre duas ou mais tabelas particionadas, as colunas de particionamento deverão ser as mesmas que as colunas nas quais as tabelas são unidas. Além disso, as tabelas ou seus índices devem ser colocados. Isso significa que eles usam a mesma função de partição nomeada ou usam funções diferentes que são essencialmente as mesmas, porque:
-  Elas têm o mesmo número de parâmetros usados para particionamento e os parâmetros correspondentes são os mesmos tipos de dados.
-  Definem o mesmo número de partições.
-  Definem os mesmos valores de limite para partições.
Desse modo, o otimizador de consulta pode processar a junção mais rapidamente, porque as próprias partições podem ser unidas. Se uma consulta unir duas tabelas que não estão colocadas ou não estão particionadas no campo de junção, a presença de partições pode realmente retardar o processamento da consulta em vez de acelerá-lo.

## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>Alterações de comportamento em computação de estatísticas durante operações de índice particionadas  
 Começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Depois de atualizar um banco de dados com índices particionados, você pode notar uma diferença nos dados de histograma destes índices. Esta alteração no comportamento pode não afetar o desempenho de consulta. Para obter as estatísticas dos índices particionados ao examinar todas as linhas da tabela, use `CREATE STATISTICS` ou `UPDATE STATISTICS` com a cláusula `FULLSCAN`.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tarefas**|**Tópico**|  
|Descreve como criar funções de partição e esquemas de partição, e depois aplicá-los a uma tabela e índice.|[Criar tabelas e índices particionados](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Você pode localizar os livros brancos a seguir em estratégias e implementações úteis de tabelas e índices particionados.  
-   [Estratégias de tabelas e índices particionados usando o SQL Server 2008](http://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)    
-   [Como implementar uma janela deslizante automática](http://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)    
-   [Carregamento em massa em uma tabela particionada](http://msdn.microsoft.com/library/cc966380.aspx)    
-   [Projeto REAL: ciclo de vida de dados -- particionamento](https://technet.microsoft.com/library/cc966424.aspx)    
-   [Aperfeiçoamentos de processamento de consultas em tabelas e índices particionados](http://msdn.microsoft.com/library/ms345599.aspx)    
-   [10 principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala](http://sqlcat.com/top10lists/archive/2008/02/06/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse.aspx)    
  
  
