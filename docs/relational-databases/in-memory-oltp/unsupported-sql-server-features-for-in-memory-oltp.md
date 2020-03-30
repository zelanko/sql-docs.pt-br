---
title: Recursos sem suporte – OLTP in-memory
ms.custom: ''
ms.date: 02/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8464f56274308694ada9e5721ae8e0ceb5ed85ed
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "77558325"
---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>Recursos do SQL Server sem suporte para OLTP na Memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este tópico discute os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com ou sem suporte para uso com objetos com otimização de memória. Além disso, a seção final lista os recursos que não tinham suporte para OLTP in-memory, mas depois passaram a ter.
  
## <a name="ssnoversion-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos sem suporte para OLTP in-memory  

Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir não têm suporte em um banco de dados que possui objetos com otimização de memória (incluindo o grupo de arquivos de dados com otimização de memória).  

  
|Recurso sem suporte|Descrição do recurso|  
|-------------------------|-------------------------|  
|Compactação de dados para tabelas com otimização de memória.|Você pode usar o recurso de compactação de dados para ajudar a compactar os dados dentro de um banco de dados e ajudar reduzir o tamanho do banco de dados. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|O particionamento de tabelas com otimização de memória, índices de HASH e índices não clusterizados.|Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).|  
| Replicação | As configurações de replicação, ao contrário da replicação transacional para tabelas com otimização de memória em assinantes, são incompatíveis com tabelas ou exibições que referenciam tabelas com otimização de memória.<br /><br />Se houver um grupo de arquivos com otimização de memória, não haverá suporte para replicação com sync_mode='database snapshot'.<br /><br />Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|
|Espelhamento|Não há suporte para o espelhamento de banco de dados para bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA. Para obter mais informações sobre espelhamento, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar log|A recompilação do log, tanto ao anexar quanto ao ALTERAR O BANCO DE DADOS, não tem suporte para bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|Você não pode acessar servidores vinculados na mesma consulta ou transação como tabelas com otimização de memória. Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).|  
|Registro em massa|Independentemente do modelo de recuperação do banco de dados, todas as operações nas tabelas duráveis com otimização de memória sempre são completamente registradas.|  
|Log mínimo|O log mínimo não tem suporte para tabelas com otimização de memória. Para obter mais informações sobre log mínimo, veja [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) e [Pré-requisitos para log mínimo na importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|controle de alterações|O controle de alterações não pode ser habilitado em um banco de dados com objetos OLTP in-memory. |
| gatilhos DDL | Os gatilhos DDL no nível de servidor e de banco de dados não têm suporte com tabelas OLTP in-memory e módulos compilados nativamente. |  
| Change Data Capture (CDC) | O SQL Server 2017 CU15 e o suporte superior habilitam o CDC em um banco de dados com tabelas otimizadas para memória. Isso só é aplicável ao banco de dados e a todas as tabelas em disco no banco de dados. Nas versões anteriores do SQL Server, o CDC não pode ser usado com um banco de dados com tabelas com otimização de memória, pois o CDC usa internamente um gatilho DDL para DROP TABLE. |  
| Modo fibra | O modo fibra não tem suporte em tabelas com otimização de memória:<br /><br />Se o modo fibra estiver ativo, não será possível criar bancos de dados com grupos de arquivos com otimização de memória ou adicionar grupos de arquivos com otimização de memória a bancos de dados existentes.<br /><br />Você pode habilitar o modo fibra se houver bancos de dados com grupos de arquivos com otimização de memória. No entanto, habilitar o modo fibra exige a reinicialização do servidor. Nessa situação, haverá falha na recuperação dos bancos de dados com grupos de arquivos com otimização de memória. Em seguida, uma mensagem de erro sugerirá que você desabilite o modo fibra para usar bancos de dados com grupos de arquivos com otimização de memória.<br /><br />Haverá falha ao anexar e restaurar bancos de dados com grupos de arquivos com otimização de memória se o modo fibra estiver ativo. Os bancos de dados será marcado como suspeito.<br /><br />Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md). |  
|Limitação do Service Broker|Não é possível acessar uma fila de um procedimento armazenado originalmente compilado.<br /><br /> Não é possível acessar uma fila em um banco de dados remoto em uma transação que acessa tabelas com otimização de memória.|  
|Replicação em assinantes|Há suporte para a replicação transacional para tabelas com otimização de memória em assinantes, mas com algumas restrições. Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)|  
|||

#### <a name="cross-database-queries-and-transcations"></a>Consultas e transações entre bancos de dados

Com algumas exceções, as transações entre bancos de dados não têm suporte. A tabela a seguir descreve os casos que têm suporte e as limitações correspondentes. (Veja também [Consultas de bancos de dados](../../relational-databases/in-memory-oltp/cross-database-queries.md).)  


|Bancos de dados|Permitido|DESCRIÇÃO|  
|---------------|-------------|-----------------|  
| Bancos de dados de usuário, **modelo** e **msdb**. | Não | Na maioria dos casos, *não* há suporte para consultas e transações entre bancos de dados.<br /><br />Uma consulta não poderá acessar outros bancos de dados se utilizar uma tabela com otimização de memória ou um procedimento armazenado compilado nativamente. Essa restrição se aplica a transações e a consultas.<br /><br />As exceções são os bancos de dados do sistema **tempdb** e **mestre**. Aqui, o banco de dados **mestre** está disponível para acesso somente leitura. |
| Banco de dados de **recursos**, **tempdb** | Sim | Em uma transação com objetos OLTP in-memory, os bancos de dados do sistema **Recurso** e **tempdb** podem ser usados sem restrição adicional.
||||

## <a name="scenarios-not-supported"></a>Cenários sem suporte  
  
- Acesso a tabelas com otimização de memória usando a conexão de contexto nos procedimentos armazenados do CLR.  
  
- Cursores dinâmicos e de conjunto de chaves em consultas que acessam tabelas com otimização de memória. Esses cursores são degradados para estático e somente leitura.  
  
- Não há suporte para usar **MERGE INTO** _target_, em que *target* é uma tabela com otimização de memória.
    - Há suporte para **MERGE USING** _source_ em tabelas com otimização de memória.  
  
- Não há suporte para o tipo de dados ROWVERSION (TIMESTAMP). Para obter mais informações, consulte [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).
  
- O fechamento automático não tem suporte nos bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.  

- Não há suporte para DDL Transacional, como CREATE/ALTER/DROP, de objetos OLTP in-memory em transações do usuário.  
  
- Notificação de eventos.  
  
- PBM (gerenciamento baseado em política).
    - Não há suporte para impedir e registrar somente modos do PBM. A existência dessas políticas no servidor pode impedir que a DDL do OLTP na memória seja executada com êxito. Há suporte para os modos sob demanda e ao agendar.  

- Não há suporte para a contenção de banco de dados ([Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)) no OLTP in-memory.
    - Há suporte para autenticação de banco de dados independente. No entanto, todos os objetos OLTP in-memory são marcados como "contenção recente" no **dm_db_uncontained_entities** da exibição de gerenciamento dinâmico (DMV).

## <a name="recently-added-supports"></a>Suportes adicionados recentemente

Às vezes, uma versão mais recente do SQL Server adiciona suporte para um recurso que não tinha suporte anteriormente. Esta seção lista recursos que costumavam não ter suporte para OLTP in-memory, mas que depois passaram a ter para OLTP in-memory.

Na tabela a seguir, os valores de _versão_ como `(15.x)` se referem ao valor retornado pela instrução Transact-SQL `SELECT @@Version;`.

| Nome do recurso | Versão do SQL Server | Comentários |
| :----------- | :-------------------- | :------- |
| Instantâneos de banco de dados | 2019 (15.x) | Os instantâneos de banco de dados agora têm suporte nos bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA. |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte Também

- [Suporte ao SQL Server para OLTP na memória](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)
