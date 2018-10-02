---
title: Especificações de capacidade máxima do SQL Server | Microsoft Docs
ms.date: 11/6/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8823f7fd346fdadfecb67c8db217894415b4e0a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764365"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Especificações de capacidade máxima do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [Especificações de capacidade máxima do SQL Server](maximum-capacity-specifications-for-sql-server.md).

  As tabelas a seguir especificam os tamanhos e números máximos de vários objetos definidos nos componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para navegar até a tabela de uma tecnologia do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , clique no respectivo link:  
  
 [Objetos do Mecanismo de Banco de Dados do SQL Server](#Engine)  
  
 [Objetos do Utilitário do SQL Server](#Utility)  
  
 [Objetos de aplicativo da camada de dados do SQL Server](#DAC)  
  
 [Objetos de Replicação do SQL Server](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] Objetos  
 Tamanhos e números máximos de vários objetos definidos nos bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou referenciados em instruções [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] objeto||Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|Informações adicionais|  
|---------------------------------------------------------|-|------------------------------------------------------------------|----------------------------|  
|Tamanho do lote||65.536 * Tamanho do pacote de rede|Tamanho do pacote de rede é o tamanho dos pacotes do protocolo TDS usados para comunicação entre aplicativos e o [!INCLUDE[ssDE](../includes/ssde-md.md)]relacional. O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.|  
|Bytes por coluna de cadeia de caracteres curta||8,000||  
|Bytes por GROUP BY, ORDER BY||8,060||  
|Bytes por chave de índice||900 bytes para um índice clusterizado. 1.700 para um índice não clusterizado.|O número máximo de bytes em qualquer chave de índice clusterizado não pode exceder 900 no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para uma chave de índice não clusterizado, o máximo é 1.700 bytes.<br /><br /> Você pode definir uma chave usando colunas de comprimento variável cujos tamanhos máximos se acumulam até mais do que o limite. No entanto, os tamanhos combinados dos dados nessas colunas nunca pode exceder o limite.<br /><br /> Em um índice não clusterizado, você pode incluir colunas adicionais não chave e não contam em relação ao limite de tamanho da chave. As colunas não chave podem ajudar algumas consultas a ter um melhor desempenho.|  
|Bytes por chave de índice para tabelas com otimização de memória||2.500 bytes para um índice não clusterizado. Nenhum limite para um índice de hash, desde que todas as chaves de índice caibam em linha.|Em uma tabela com otimização de memória, um índice não clusterizado não pode ter colunas de chave cujos tamanhos máximos de declarados excedem 2.500 bytes. É irrelevante se os dados reais nas colunas de chave são menores que os tamanhos máximos declarados.<br /><br /> Para uma chave de índice de hash, não há um limite fixo no tamanho.<br /><br /> Para índices em tabelas com otimização de memória, não há nenhum conceito de colunas incluídas, pois inerentemente todos os índices abrangem todas as colunas.<br /><br /> Para uma tabela com otimização de memória, mesmo que o tamanho da linha seja 8.060 bytes, algumas colunas de comprimento variável podem ser fisicamente armazenadas fora desses 8.060 bytes. No entanto, os tamanhos máximos declarados de todas as colunas de chave para todos os índices em uma tabela, além de quaisquer colunas de comprimento fixo adicionais, devem caber nos 8.060 bytes.|  
|Bytes por chave estrangeira||900||  
|Bytes por chave primária||900||  
|Bytes por linha||8.060|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte ao armazenamento de estouro de linha, o que permite que colunas de comprimento variável sejam enviadas por push para fora da linha. Somente uma raiz de 24 bytes é armazenada no registro principal para colunas de comprimento variável empurradas para fora da linha; por isso, o limite efetivo de linha é maior que nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte o tópico "Dados de estouro de linha que excedem 8 KB" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|Bytes por linha em tabelas com otimização de memória||8,060|Começando no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , as tabelas com otimização de memória dão suporte ao armazenamento fora da linha. Colunas de comprimento variável são enviadas por push para fora da linha se os tamanhos máximos de todas as colunas na tabela excederem 8.060 bytes. Esta é uma decisão de tempo de compilação. Apenas uma referência de 8 bytes é armazenada na linha para colunas armazenadas fora de linha. Para obter mais informações, consulte [Tamanho da tabela e da linha em tabelas com otimização de memória](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|  
|Bytes em texto de fonte de um procedimento armazenado||Menor que o tamanho do lote ou 250 MB||  
|Bytes por coluna **varchar(max)**, **varbinary(max)**, **xml**, **text**ou **image**||2^31-1||  
|Caracteres por coluna **ntext** ou **nvarchar(max)**||2^30-1||  
|Índices clusterizados por tabela||1||  
|Colunas em GROUP BY, ORDER BY||Limitado somente pelo número de bytes||  
|Colunas ou expressões em uma instrução GROUP BY WITH CUBE ou WITH ROLLUP||10||  
|Colunas por chave de índice||32|Se a tabela contiver um ou mais índices XML, a chave de clustering da tabela do usuário será limitada a 31 colunas porque a coluna XML é adicionada à chave de clustering do índice XML primário. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você pode incluir colunas não chave em um índice não clusterizado para evitar a limitação de um máximo de 32 colunas de chave. Para obter mais informações, consulte [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md).|  
|Colunas por chave estrangeira||32||  
|Colunas por chave primária||32||  
|Colunas por tabela não larga||1,024||  
|Colunas por tabela larga||30,000||  
|Colunas por instrução SELECT||4,096||  
|Colunas por instrução INSERT||4,096||  
|Conexões por cliente||Valor máximo de conexões configuradas||  
|Tamanho do banco de dados||524.272 terabytes||  
|Bancos de dados por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||32,767||  
|Grupos de arquivos por banco de dados||32,767||  
|Grupos de arquivo por banco de dados para dados com otimização de memória.||1||  
|Arquivos por banco de dados||32,767||  
|Tamanho de arquivo (dados)||16 terabytes||  
|Tamanho de arquivo (log)||2 terabytes||  
|Arquivos de dados para dados com otimização de memória por banco de dados||4.096 no [!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)]. As versões posteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não impõem um limite estrito como esse.||  
|Arquivo delta por arquivo de dados para dados com otimização de memória||1||  
|Referências de tabela de chave estrangeira por tabela||Saída = 253. Entrada= 10.000.|Para restrições, consulte [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md).|  
|Comprimento de identificador (em caracteres)||128||  
|Instâncias por computador||50 instâncias em um servidor autônomo.<br /><br /> 25 instâncias em um cluster de failover ao usar um disco de cluster compartilhado como a opção de armazenamento para sua instalação de cluster. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dará suporte a 50 instâncias de um cluster de failover se você escolher compartilhamentos de arquivos SMB como a opção de armazenamento para seu cluster de failover.||  
|Índices por tabela com otimização de memória||999 a partir do [!INCLUDE[ssSQL17](../includes/ssSQL17-md.md)] e no [!INCLUDE[ssSDSFull](../includes/ssSDSFull-md.md)]<br/>8 no [!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)] e [!INCLUDE[ssSQL15](../includes/ssSQL15-md.md)]||  
|Comprimento de uma cadeia de caracteres que contém instruções SQL (tamanho do lote)||65.536 * Tamanho do pacote de rede|Tamanho do pacote de rede é o tamanho dos pacotes do protocolo TDS usados para comunicação entre aplicativos e o [!INCLUDE[ssDE](../includes/ssde-md.md)]relacional. O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.|  
|Bloqueios por conexão||Máximo de bloqueios por servidor||  
|Bloqueios por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||Limitado somente por memória|Esse valor é para alocação de bloqueio estático. Os bloqueios dinâmicos são limitados somente por memória.|  
|Níveis aninhados de procedimento armazenado||32|Se um procedimento armazenado acessar mais de 64 bancos de dados ou mais de 2 bancos de dados em intercalação, você receberá um erro.|  
|Subconsultas aninhadas||32||  
|Níveis aninhados de gatilho||32||  
|Índices não clusterizados por tabela||999||  
|Número de expressões distintas na cláusula GROUP BY quando qualquer um dos seguintes estiver presente: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP||32||  
|Número de conjuntos de agrupamentos gerados por operadores na cláusula GROUP BY||4,096||  
|Parâmetros por procedimento armazenado||2,100||  
|Parâmetros por função definida pelo usuário||2,100||  
|REFERENCES por tabela||253||  
|Linhas por tabela||Limitado pelo armazenamento disponível||  
|Tabelas por banco de dados||Limitado pelo número de objetos em um banco de dados|Os objetos de banco de dados incluem objetos como tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, gatilhos, regras, padrões e restrições. A soma do número de todos os objetos em um banco de dados não pode exceder 2.147.483.647.|  
|Partições por tabela ou índice particionado||15,000||  
|Estatísticas em colunas não indexadas||30,000|| 
|Tabelas por instrução SELECT||Limitado apenas pelos recursos disponíveis||  
|Gatilhos por tabela||Limitado pelo número de objetos em um banco de dados|Os objetos de banco de dados incluem objetos como tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, gatilhos, regras, padrões e restrições. A soma do número de todos os objetos em um banco de dados não pode exceder 2.147.483.647.|  
|Colunas por instrução UPDATE (Tabelas Largas)||4096||  
|Conexões de usuário||32,767||  
|índices XML||249||  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos do utilitário  
 Tamanhos e números máximos de vários objetos que foram testados no Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto do utilitário||Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|----------------------------------------------|-|------------------------------------------------------------------|  
|Computadores (computadores físicos ou máquinas virtuais) por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||100|  
|Instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por computador||5|  
|Número total de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||200*|  
|Bancos de dados de usuários por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], inclusive aplicativos da camada de dados||50|  
|Número total de bancos de dados de usuário por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||1,000|  
|Grupos de arquivos por banco de dados||1|  
|Arquivos de dados por grupo de arquivos||1|  
|Arquivos de log por banco de dados||1|  
|Volumes por computador||3|  
  
 *O número máximo de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com suporte do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode variar com base na configuração de hardware do servidor. Para obter informações de introdução, consulte [Recursos e tarefas do utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não está disponível em todas as edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx).    
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de aplicativo da camada de dados  
 Tamanhos e números máximos de vários objetos que foram testados nos DAC (aplicativos de camada de dados) do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC||Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|------------------------------------------|-|------------------------------------------------------------------|  
|Bancos de dados por DAC||1|  
|Objetos por DAC*||Limitado pelo número de objetos em um banco de dados ou pela memória disponível.|  
  
 *Os tipos de objetos incluídos no limite são usuários, tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, tipo de dados definido pelo usuário, funções de banco de dados, esquemas e tipos de tabela definidos pelo usuário.  
  
##  <a name="Replication"></a> Objetos de replicação  
 Tamanhos e números máximos de vários objetos definidos na Replicação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de replicação||Tamanhos/números máximos do SQL Server (64 bits)|  
|--------------------------------------------------|-|---------------------------------------------------|  
|Artigos (publicação de mesclagem)||2048|  
|Artigos (publicação de instantâneo ou transacional)||32,767|  
|Colunas em uma tabela* (publicação de mesclagem)||246|  
|Colunas em uma tabela** (instantâneo do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou publicação transacional)||1,000|  
|Colunas em uma tabela** (instantâneo do Oracle ou publicação transacional)||995|  
|Bytes para uma coluna usada em um filtro de linha (publicação de mesclagem)||1,024|  
|Bytes para uma coluna usada em um filtro de linha (publicação de instantâneo ou transacional)||8,000|  

 *Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo para que um máximo de 246 colunas seja publicado. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
 **A tabela base pode incluir o número máximo de colunas permitidas no banco de dados de publicação (1.024 para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), mas as colunas devem ser filtradas do artigo se excederem o máximo especificado para o tipo de publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Verificar parâmetros do Verificador de Configuração do Sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Recursos e tarefas do utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
