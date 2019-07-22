---
title: Diretrizes para operações de índice online | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6a2266a83d8fb041f4d18c5938e87bf31433b70e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909796"
---
# <a name="guidelines-for-online-index-operations"></a>Diretrizes para operações de índice online

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Quando você executa operações de índice online, as diretrizes seguintes se aplicam:  

- Os índices clusterizados devem ser criados, recriados ou descartados offline quando a tabela subjacente contiver estes tipos de dados LOB (objeto grande): **image**, **ntext**e **text**.  
- Índices não clusterizados não exclusivos podem ser criados online, quando a tabela contiver tipos de dados LOB, mas nenhuma dessas colunas são usadas na definição de índice seja como colunas-chaves ou colunas não chave.  
- Os índices em tabelas temporárias locais, não podem ser criados, recriados ou soltos offline. Esta restrição não se aplica a índices em tabelas temporárias globais.
- Índices podem ser retomados de onde pararam após uma falha inesperada, failover de banco de dados ou um comando **PAUSE**. Consulte [Criar índice](../../t-sql/statements/create-index-transact-sql.md) e [Alterar índice](../../t-sql/statements/alter-index-transact-sql.md).

> [!NOTE]  
> As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte pelas edições](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  

A tabela seguinte mostra os operações de índice que podem ser executadas online e os índices que são excluídos destas operações online, além das restrições de índice resumíveis. Restrições adicionais também estão incluídas.  

| Operação de índice online | Índices excluídos | Outras restrições |  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|Índice clusterizado desabilitado ou exibição indexada desabilitada<br /><br /> Índice XML<br /><br />Índice columnstore <br /><br /> Índice em uma tabela temporária local|Especificar a palavra-chave ALL pode fazer com que a operação falhe, quando a tabela contiver um índice excluído.<br /><br /> Se aplicam as restrições adicionais na reconstrução de índices desabilitados. Para obter mais informações, consulte [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md).|  
|CREATE INDEX|Índice XML<br /><br /> Índice clusterizado exclusivo inicial em uma exibição<br /><br /> Índice em uma tabela temporária local||  
|CREATE INDEX WITH DROP_EXISTING|Índice clusterizado desabilitado ou exibição indexada desabilitada<br /><br /> Índice em uma tabela temporária local<br /><br /> Índice XML||  
|DROP INDEX|Índice desabilitado<br /><br /> Índice XML<br /><br /> Índice não clusterizado<br /><br /> Índice em uma tabela temporária local|Os índices múltiplos não podem ser especificados dentro de uma única declaração.|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY ou UNIQUE)|Índice em uma tabela temporária local<br /><br /> Índice clusterizado|Somente um subcláusula por vez é permitida. Por exemplo, você não pode acrescentar e soltar restrições PRIMARY KEY ou UNIQUE na mesma declaração ALTER TABLE.|  
|ALTER TABLE DROP CONSTRAINT (PRIMARY KEY ou UNIQUE)|Índice clusterizado||  
  
 A tabela subjacente não pode ser modificada, truncada ou solta enquanto uma operação de índice online está em curso.  
  
 A configuração especificada de opção online (ON ou OFF) quando você cria ou solta um índice clusterizado é aplicada a qualquer índice não clusterizado que deva ser reconstruído. Por exemplo, se o índice clusterizado for construído online usando CREATE INDEX WITH DROP_EXISTING, ONLINE=ON, todos os índices não clusterizados associados também serão recriados.  
  
 Quando você cria ou reconstrói um índice UNIQUE online, o construtor de índice e uma transação de usuário simultânea podem tentar inserir a mesma chave, e, portanto, violando a singularidade. Se uma fila digitada por um usuário é inserida no índice novo (destino) antes que a fila original da tabela de destino seja movida para o índice novo, a operação de índice online falhará.  
  
 Embora não seja comum, a operação de índice online pode causar um deadlock quando interagir com as atualizações do banco de dados por causa das atividades de usuário ou aplicativo. Nesses raros casos, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] irá selecionar a atividade do usuário ou aplicativo como uma vítima de deadlock.  
  
 Você pode executar operações DDL simultâneas de índice online na mesma tabela ou apenas exibi-las quando estiver criando vários índices não clusterizados novos, ou reorganizando índices não clusterizados. Todas as outras operações de índice online executadas ao mesmo tempo falham. Por exemplo, você não pode criar um novo índice online enquanto estiver reconstruindo um índice online existente na mesma tabela.  
  
 Uma operação online não pode ser efetuada quando um índice contém uma coluna de um tipo de objeto grande, e na mesma transação há operações de atualização anteriores a essa operação online. Para resolver esse problema, coloque a operação online fora da transação ou coloque-a antes de quaisquer atualizações na transação.  
  
## <a name="disk-space-considerations"></a>Considerações do espaço em disco

As operações de índice online exigem mais requisitos de espaço em disco que operações de índice offline.

- Durante a criação de índice e as operações de recompilação de índice, o espaço adicional é necessário para o índice que está sendo criado (ou recompilado).
- Além disso, o espaço em disco é necessário para o índice de mapeamento temporário. Este índice temporário é usado em operações de índice online que criam, reconstroem, ou soltam um índice clusterizado.
- Remover um índice clusterizado online requer tanto espaço quanto criar (ou recriar) um índice clusterizado online.

Para obter mais informações, consulte [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho

Embora as operações de índice online permitam atividade de atualização de usuário simultânea, as operações de índice levarão mais tempo se a atividade de atualização for muito pesada. Tipicamente, as operações de índice online serão mais lentas que as operações de índice offline equivalentes, independentemente do nível de atividade de atualização simultâneo.  
  
Em razão de ambas as estruturas de fonte e destino serem mantidas durante a operação de índice online, o uso de recurso para as operações de inserção, atualização e exclusão é aumentado, potencialmente até o dobro. Isto poderia causar uma diminuição no desempenho e maior uso de recurso, especialmente tempo de CPU, durante a operação de índice. As operações de índice online estão em log completo.  
  
Embora recomendemos as operações online , você deve avaliar o seu ambiente e os requisitos específicos. Pode ser melhor executar as operações de índice offline. Fazendo isto, os usuários têm acesso restrito aos dados durante a operação, mas a operação termina mais rapidamente e usa menos recursos.  
  
Em computadores multiprocessadores em execução no SQL Server 2016, as instruções de índice podem usar mais processadores para executar operações de exame e classificação associadas à instrução de índice da mesma forma que outras consultas. Você pode usar a opção de índice MAXDOP para controlar o número de processadores dedicados a uma operação de índice online. Desse modo, é possível equilibrar os recursos usados por uma operação de índice com aqueles dos usuários simultâneos. Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md). Para mais informações sobre as edições do SQL Server que dão suporte a operações indexadas paralelas, consulte [Recursos compatíveis com as edições](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
Em razão do bloqueio S-lock ou Sch-M ser mantido na fase final da operação de índice, tome cuidado ao executar uma operação de índice online dentro de uma transação de usuário explicita, como no bloco BEGIN TRANSACTION...COMMIT. Fazer isso faz com que a fechadura seja mantida até o término da transação, impedindo portanto simultaneidade de usuário.  
  
A recriação de índice online pode aumentar a fragmentação quando é permitido executá-la com as opções `MAX DOP > 1` e `ALLOW_PAGE_LOCKS = OFF` . Para obter mais informações, confira [Como funciona: Recompilação de Índice Online – Pode causar maior fragmentação](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx).  
  
## <a name="transaction-log-considerations"></a>Considerações do log de transações

As operações de índice em larga escala, executadas offline ou online, podem gerar grandes cargas de dados que podem fazer com que o log de transações seja preenchido rapidamente. Para assegurar que a operação de índice possa ser revertida, o log de transações não pode ser truncado até que a operação de índice se complete. Durante a operação de índice, no entanto, poderá ser feito backup do log. Portanto, o log de transações deve ter espaço suficiente para armazenar as transações da operação de índice e quaisquer transações simultâneas de usuário pelo período da operação de índice. Para obter mais informações, consulte [Espaço em disco de log de transações para operações de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md).  

## <a name="resumable-index-considerations"></a>Considerações de índice retomável

> [!NOTE]
> A opção de índice retomável aplica-se ao SQL Server (começando com o SQL Server 2017) (somente a recompilação de índice) e o Banco de Dados SQL (criação de índice e recompilação de índice). Consulte [Criar Índice](../../t-sql/statements/create-index-transact-sql.md) (no momento, em versão prévia pública para [!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)]) e [Alterar Índice](../../t-sql/statements/alter-index-transact-sql.md).

Quando você executa a criação ou a recriação de índice online retomável, as seguintes diretrizes se aplicam:

- Gerenciamento, planejamento e extensão das janelas de manutenção de índice. Você pode pausar e reiniciar uma operação de criação ou recriação de índice várias vezes para adequar-se às janelas de manutenção.
- Recuperação de falhas de criação ou recriação de índice (tais como failovers de banco de dados ou ficar sem espaço em disco).
- Quando uma operação de índice está em pausa, tanto o índice original quanto um recém-criado exigem espaço em disco e precisam ser atualizados durante as operações de DML.
- Habilita o truncamento de logs de transações durante uma operação de criação ou recompilação de índice.
- A opção SORT_IN_TEMPDB=ON não é compatível

> [!IMPORTANT]
> A criação ou a recriação retomável não exige que você mantenha aberta uma transação de longa execução, permitindo o truncamento de log durante essa operação e um melhor gerenciamento do espaço de log. Com o novo design, conseguimos manter os dados necessários em um banco de dados junto com todas as referências necessárias para reiniciar a operação retomável.

Em geral, não há nenhuma diferença de desempenho entre a recompilação de índice online retomável e não retomável. Para criar o índice retomável, há uma sobrecarga de constante que causa uma pequena diferença no desempenho entre a criação dos índices retomável e não retomável. Essa diferença é bastante notável apenas para tabelas menores.

Quando você atualiza um índice retomável enquanto uma operação de índice está em pausa:

- Para cargas de trabalho primariamente de leitura, o impacto no desempenho é irrisório.
- Para cargas de trabalho com atualização intensa, você pode observar certa degradação da taxa de transferência (nossos testes mostram menos de 10% de degradação).

Em geral, não há nenhuma diferença na qualidade de desfragmentação entre a criação ou a recriação de índice online retomável e não retomável.

## <a name="online-default-options"></a>Opções online padrão

> [!IMPORTANT]
> Essas opções estão em versão prévia pública para [!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)].

Você pode definir opções padrão para online ou retomáveis em um nível de banco de dados, definindo as opções de configuração com escopo do banco de dados ELEVATE_ONLINE ou ELEVATE_RESUMABLE. Com essas opções padrão, você pode evitar a execução acidental de uma operação que deixa a tabela do banco de dados offline. Ambas as opções farão com que o mecanismo eleve automaticamente determinadas operações para execução online ou retomável.  
Você pode definir qualquer uma das opções como FAIL_UNSUPPORTED, WHEN_SUPPORTED ou OFF usando o comando [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Você pode definir valores diferentes para online e retomável.

ELEVATE_ONLINE e ELEVATE_RESUMABLE são aplicáveis somente a instruções DDL que dão suporte à sintaxe online e retomável respectivamente. Por exemplo, se você tentar criar um índice XML com ELEVATE_ONLINE=FAIL_UNSUPORTED, a operação será executada offline, pois os índices XML não dão suporte à sintaxe ONLINE=. As opções somente afetam as instruções DDL enviadas sem especificar uma opção ONLINE ou RESUMABLE. Por exemplo, ao enviar uma instrução com ONLINE=OFF ou RESUMABLE=OFF, o usuário pode substituir uma configuração FAIL_UNSUPPORTED e executar uma instrução offline e/ou de modo não retomável.

> [!NOTE]
> ELEVATE_ONLINE e ELEVATE_RESUMABLE não se aplicam a operações de índice XML.

## <a name="related-content"></a>Conteúdo relacionado

- [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md)  
- [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)  
- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
