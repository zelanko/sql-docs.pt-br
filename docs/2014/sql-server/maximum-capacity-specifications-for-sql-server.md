---
title: Especificações de capacidade máxima do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
ms.openlocfilehash: 59b45d3ab221e02b89abf328eac5f189f0f84728
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044586"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Especificações de capacidade máxima do SQL Server
  As tabelas a seguir especificam os tamanhos e números máximos de vários objetos definidos nos componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para navegar até a tabela de uma tecnologia do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , clique no respectivo link:  
  
 [Objetos do Mecanismo de Banco de Dados do SQL Server](#Engine)  
  
 [Objetos do Utilitário do SQL Server](#Utility)  
  
 [Objetos de aplicativo da camada de dados do SQL Server](#DAC)  
  
 [Objetos de Replicação do SQL Server](#Replication)  
  
##  <a name="ssde-objects"></a><a name="Engine"></a>[!INCLUDE[ssDE](../includes/ssde-md.md)]Objetos do  
 A tabela a seguir especifica os tamanhos e números máximos de vários objetos definidos nos bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou referenciados em instruções [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
|Objeto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]|Tamanhos/números máximos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Tamanho do lote<br /><br /> Observação: o tamanho do pacote de rede é o tamanho dos pacotes TDS usados para comunicação entre os aplicativos e o relacional [!INCLUDE[ssDE](../includes/ssde-md.md)] . O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.|65.536 * Tamanho do pacote de rede|65.536 * Tamanho do pacote de rede|  
|Bytes por coluna de cadeia de caracteres curta|8,000|8,000|  
|Bytes por GROUP BY, ORDER BY|8,060|8,060|  
|Bytes por chave de índice<br /><br /> Observação: o número máximo de bytes em qualquer chave de índice não pode exceder 900 em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Você pode definir uma chave usando colunas de comprimento variável cujos tamanhos máximos somem mais de 900, desde que nenhuma linha jamais seja inserida com mais de 900 bytes de dados nessas colunas. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você pode incluir colunas não chave em um índice não clusterizado para evitar o tamanho máximo de chave de índice de 900 bytes.|900|900|  
|Bytes por chave estrangeira|900|900|  
|Bytes por chave primária|900|900|  
|Bytes por linha<br /><br /> Observação:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte ao armazenamento de estouro de linha, o que permite que colunas de comprimento variável sejam enviadas por push para fora da linha. Somente uma raiz de 24 bytes é armazenada no registro principal para colunas de comprimento variável empurradas para fora da linha; por isso, o limite efetivo de linha é maior que nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte o tópico "Dados de estouro de linha que excedem 8 KB" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|8,060|8,060|  
|Bytes por linha em tabelas com otimização de memória<br /><br /> Observação:<br />        OLTP na memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não oferece suporte ao armazenamento de estouro de linha. As colunas de comprimento variável não são retiradas da linha. Isso limita a largura máxima de colunas de comprimento variável que você pode especificar em uma tabela com otimização de memória para o tamanho máximo da linha. Para obter mais informações, consulte [Tamanho da tabela e da linha em tabelas com otimização de memória](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|Sem suporte|8,060|  
|Bytes em texto de fonte de um procedimento armazenado|Menor que o tamanho do lote ou 250 MB|Menor que o tamanho do lote ou 250 MB|  
|Bytes por coluna `varchar(max)`, `varbinary(max)`, `xml`, `text` ou `image`|2^31-1|2^31-1|  
|Caracteres por coluna `ntext` ou `nvarchar(max)`|2^30-1|2^30-1|  
|Índices clusterizados por tabela|1|1|  
|Colunas em GROUP BY, ORDER BY|Limitado somente pelo número de bytes|Limitado somente pelo número de bytes|  
|Colunas ou expressões em uma instrução GROUP BY WITH CUBE ou WITH ROLLUP|10|10|  
|Colunas por chave de índice<br /><br /> Observação: se a tabela contiver um ou mais índices XML, a chave de clustering da tabela de usuário será limitada a 15 colunas porque a coluna XML é adicionada à chave de clustering do índice XML primário. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você pode incluir colunas não chave em um índice não clusterizado para evitar a limitação de um máximo de 16 colunas de chave. Para obter mais informações, consulte [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md).|16|16|  
|Colunas por chave estrangeira|16|16|  
|Colunas por chave primária|16|16|  
|Colunas por tabela não larga|1\.024|1\.024|  
|Colunas por tabela larga|30,000|30,000|  
|Colunas por instrução SELECT|4\.096|4\.096|  
|Colunas por instrução INSERT|4096|4096|  
|Conexões por cliente|Valor máximo de conexões configuradas|Valor máximo de conexões configuradas|  
|Tamanho do banco de dados|524.272 terabytes|524.272 terabytes|  
|Bancos de dados por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32.767|32.767|  
|Grupos de arquivos por banco de dados|32.767|32.767|  
|Grupos de arquivo por banco de dados para dados com otimização de memória.|Sem suporte|1|  
|Arquivos por banco de dados|32.767|32.767|  
|Tamanho de arquivo (dados)|16 terabytes|16 terabytes|  
|Tamanho de arquivo (log)|2 terabytes|2 terabytes|  
|Arquivos de dados para dados com otimização de memória por banco de dados|Sem suporte|4.096|  
|Arquivo delta por arquivo de dados para dados com otimização de memória|Sem suporte|1|  
|Referências de tabela de chave estrangeira por tabela<br /><br /> Observação: embora uma tabela possa conter um número ilimitado de restrições FOREIGN KEY, o máximo recomendado é 253. Dependendo da configuração do hardware que hospeda o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a especificação de restrições FOREIGN KEY adicionais pode ser cara para processamento pelo otimizador de consulta.|253|253|  
|Comprimento de identificador (em caracteres)|128|128|  
|Instâncias por computador|50 instâncias em um servidor autônomo para todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]dá suporte a 25 instâncias em um cluster de failover ao usar um disco de cluster compartilhado, pois a opção armazenada para a instalação de cluster é [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatível com 50 instâncias em um cluster de failover se você escolher compartilhamentos de arquivos SMB como a opção de armazenamento para a instalação do cluster para obter mais informações, consulte [requisitos de hardware e software para instalar SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md).|50 instâncias em um servidor autônomo.<br /><br /> 25 instâncias em um cluster de failover ao usar um disco de cluster compartilhado como a opção de armazenamento para sua instalação de cluster. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dará suporte a 50 instâncias de um cluster de failover se você escolher compartilhamentos de arquivos SMB como a opção de armazenamento para seu cluster de failover.|  
|Índices por tabela com otimização de memória|Sem suporte|8|  
|Comprimento de uma cadeia de caracteres que contém instruções SQL (tamanho do lote)<br /><br /> Observação: o tamanho do pacote de rede é o tamanho dos pacotes TDS usados para comunicação entre os aplicativos e o relacional [!INCLUDE[ssDE](../includes/ssde-md.md)] . O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.|65.536 * Tamanho do pacote de rede|65.536 * Tamanho do pacote de rede|  
|Bloqueios por conexão|Máximo de bloqueios por servidor|Máximo de bloqueios por servidor|  
|Bloqueios por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> Observação: esse valor é para alocação de bloqueio estático. Os bloqueios dinâmicos são limitados somente por memória.|Até 2.147.483.647|Limitado somente por memória|  
|Níveis aninhados de procedimento armazenado<br /><br /> Observação: se um procedimento armazenado acessar mais de 64 bancos de dados ou mais de 2 bancos de dados na intercalação, você receberá um erro.|32|32|  
|Subconsultas aninhadas|32|32|  
|Níveis aninhados de gatilho|32|32|  
|Índices não clusterizados por tabela|999|999|  
|Número de expressões distintas na cláusula GROUP BY quando qualquer um dos seguintes estiver presente: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP|32|32|  
|Número de conjuntos de agrupamentos gerados por operadores na cláusula GROUP BY|4\.096|4\.096|  
|Parâmetros por procedimento armazenado|2,100|2,100|  
|Parâmetros por função definida pelo usuário|2,100|2,100|  
|REFERENCES por tabela|253|253|  
|Linhas por tabela|Limitado pelo armazenamento disponível|Limitado pelo armazenamento disponível|  
|Tabelas por banco de dados<br /><br /> Observação: os objetos de banco de dados incluem objetos como tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, gatilhos, regras, padrões e restrições. A soma do número de todos os objetos em um banco de dados não pode exceder 2.147.483.647.|Limitado pelo número de objetos em um banco de dados|Limitado pelo número de objetos em um banco de dados|  
|Partições por tabela ou índice particionado|1,000<br /><br /> Importante a criação de uma tabela ou um índice com mais de 1.000 partições é possível em um sistema de 32 bits, mas não tem suporte. ** \* \* \* \* **|15,000|  
|Estatísticas em colunas não indexadas|30,000|30,000|  
|Tabelas por instrução SELECT|Limitado apenas pelos recursos disponíveis|Limitado apenas pelos recursos disponíveis|  
|Gatilhos por tabela<br /><br /> Observação: os objetos de banco de dados incluem objetos como tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, gatilhos, regras, padrões e restrições. A soma do número de todos os objetos em um banco de dados não pode exceder 2.147.483.647.|Limitado pelo número de objetos em um banco de dados|Limitado pelo número de objetos em um banco de dados|  
|Colunas por instrução UPDATE (Tabelas Largas)|4096|4096|  
|Conexões de usuário|32.767|32.767|  
|índices XML|249|249|  
  
##  <a name="ssnoversion-utility-objects"></a><a name="Utility"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Objetos do utilitário  
 A tabela a seguir especifica os tamanhos e números máximos de vários objetos que foram testados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto do utilitário|Tamanhos/números máximos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Computadores (computadores físicos ou máquinas virtuais) por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|100|100|  
|Instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por computador|5|5|  
|Número total de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|200*|200*|  
|Bancos de dados de usuários por instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], inclusive aplicativos da camada de dados|50|50|  
|Número total de bancos de dados de usuário por Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|1,000|1,000|  
|Grupos de arquivos por banco de dados|1|1|  
|Arquivos de dados por grupo de arquivos|1|1|  
|Arquivos de log por banco de dados|1|1|  
|Volumes por computador|3|3|  
  
 * O número máximo de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com suporte pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilitário pode variar com base na configuração de hardware do servidor. Para obter informações de introdução, consulte [Recursos e tarefas do utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]o ponto de controle do utilitário não está disponível em todas as edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
##  <a name="ssnoversion-data-tier-application-objects"></a><a name="DAC"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Objetos de aplicativo da camada de dados  
 A tabela a seguir especifica os tamanhos e números máximos de vários objetos que foram testados nos DACs (aplicativos da camada de dados) do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC|Tamanhos/números máximos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamanho máximo/números [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Bancos de dados por DAC|1|1|  
|Objetos por DAC*|Limitado pelo número de objetos em um banco de dados ou pela memória disponível.|Limitado pelo número de objetos em um banco de dados ou pela memória disponível.|  
  
 *Os tipos de objetos incluídos no limite são usuários, tabelas, exibições, procedimentos armazenados, funções definidas pelo usuário, tipo de dados definido pelo usuário, funções de banco de dados, esquemas e tipos de tabela definidos pelo usuário.  
  
##  <a name="replication-objects"></a><a name="Replication"></a>Objetos de replicação  
 A tabela a seguir especifica os tamanhos e números máximos de vários objetos definidos na Replicação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de replicação|Tamanhos/números máximos do SQL Server (32 bits)|Tamanhos/números máximos do SQL Server (64 bits)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|Artigos (publicação de mesclagem)|256|256|  
|Artigos (publicação de instantâneo ou transacional)|32.767|32.767|  
|Colunas em uma tabela* (publicação de mesclagem)|246|246|  
|Colunas em uma tabela** (instantâneo do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou publicação transacional)|1,000|1,000|  
|Colunas em uma tabela** (instantâneo do Oracle ou publicação transacional)|995|995|  
|Bytes para uma coluna usada em um filtro de linha (publicação de mesclagem)|1\.024|1\.024|  
|Bytes para uma coluna usada em um filtro de linha (publicação de instantâneo ou transacional)|8,000|8,000|  
  
 *Se o controle de linha for usado para detecção de conflitos (o padrão), a tabela base poderá incluir no máximo 1.024 colunas, mas as colunas deverão ser filtradas do artigo para que um máximo de 246 colunas seja publicado. Se o rastreamento de coluna for usado, a tabela base poderá incluir no máximo 246 colunas.  
  
 **A tabela base pode incluir o número máximo de colunas permitidas no banco de dados de publicação (1.024 para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), mas as colunas devem ser filtradas do artigo se excederem o máximo especificado para o tipo de publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos de hardware e software para a instalação do SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Verificar parâmetros para o verificador de configuração do sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Recursos e tarefas do Utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
