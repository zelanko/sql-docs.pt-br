---
title: "Diretrizes para operações de índice online | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.suite: SQL
ms.prod_service: database engine, sql database, sql data warehouse
ms.component: indexes
ms.translationtype: HT
ms.sourcegitcommit: 0c85f3e3417afc5943baee86eff0c3248172f82a
ms.openlocfilehash: 9b6d3aabe451c35c25822a2114e825e980ad01d3
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="guidelines-for-online-index-operations"></a>Diretrizes para operações de índice online
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quando você executa operações de índice online, as diretrizes seguintes se aplicam:  
  
-   Os índices clusterizados devem ser criados, recriados ou descartados offline quando a tabela subjacente contiver estes tipos de dados LOB (objeto grande): **image**, **ntext**e **text**.  
  
-   Índices não clusterizados não exclusivos podem ser criados online, quando a tabela contiver tipos de dados LOB, mas nenhuma dessas colunas são usadas na definição de índice seja como colunas-chaves ou colunas não chave.  
  
-   Os índices em tabelas temporárias locais, não podem ser criados, recriados ou soltos offline. Esta restrição não se aplica a índices em tabelas temporárias globais.
- Índices podem ser retomados de onde pararam após uma falha inesperada, failover de banco de dados ou um comando **PAUSE**. Consulte [Alterar Índice](../../t-sql/statements/alter-index-transact-sql.md). Este recurso está em visualização pública para o SQL Server 2017 e o Banco de Dados SQL do Azure.

> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte pelas edições](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
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
  
 A recriação de índice online pode aumentar a fragmentação quando é permitido executá-la com as opções `MAX DOP > 1` e `ALLOW_PAGE_LOCKS = OFF` . Para obter mais informações, consulte [Como funciona: recriação de índice online - pode causar maior fragmentação](http://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx).  
  
## <a name="transaction-log-considerations"></a>Considerações do log de transações  
 As operações de índice em larga escala, executadas offline ou online, podem gerar grandes cargas de dados que podem fazer com que o log de transações seja preenchido rapidamente. Para assegurar que a operação de índice possa ser revertida, o log de transações não pode ser truncado até que a operação de índice se complete. Durante a operação de índice, no entanto, poderá ser feito backup do log. Portanto, o log de transações deve ter espaço suficiente para armazenar as transações da operação de índice e quaisquer transações simultâneas de usuário pelo período da operação de índice. Para obter mais informações, consulte [Espaço em disco de log de transações para operações de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md).  

## <a name="resumable-index-rebuild-considerations"></a>Considerações de recompilação de índice retomáveis

> [!NOTE]
> Consulte [Alterar Índice](../../t-sql/statements/alter-index-transact-sql.md). Este recurso está em visualização pública para o SQL Server 2017 e o Banco de Dados SQL do Azure.
>

As diretrizes a seguir se aplicam ao executar a recompilação de índice online retomável:
-   Gerenciamento, planejamento e extensão das janelas de manutenção de índice. Você pode pausar e reiniciar uma operação de recompilação de índice várias vezes para adequar-se às janelas de manutenção.
- Recuperação de falhas de recompilação de índice (tais como failovers de banco de dados ou falta de espaço em disco).
- Quando uma operação de índice está em pausa, tanto o índice original quanto um recém-criado exigem espaço em disco e precisam ser atualizados durante as operações de DML.

- Habilita o truncamento de logs durante uma operação de recompilação de índice (esta operação não pode ser realizada para uma operação de índice online regular).
- A opção SORT_IN_TEMPDB=ON não é compatível

> [!IMPORTANT]
> A recompilação retomável não exige que você mantenha aberto um truncamento de longa execução, permitindo o truncamento de log durante essa operação e um melhor gerenciamento do espaço de log. Com o novo design, conseguimos manter os dados necessários em um banco de dados junto com todas as referências necessárias para reiniciar a operação retomável.
>

Em geral, não há nenhuma diferença de desempenho entre a recompilação de índice online retomável e não retomável. Quando você atualiza um índice retomável enquanto uma operação de recompilação de índice está em pausa:
- Para cargas de trabalho primariamente de leitura, o impacto no desempenho é insignificante. 
- Para cargas de trabalho com atualização intensa, você pode observar certa degradação da taxa de transferência (nossos testes mostram menos de 10% de degradação).

Em geral, não há nenhuma diferença na qualidade de desfragmentação entre a recompilação de índice online retomável e não retomável.
 
## <a name="related-content"></a>Conteúdo relacionado  
 [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md)  
  
 [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  

