---
description: Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória
title: Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 23274522-e5cf-4095-bed8-bf986d6342e0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f8aaedc07aef085f7245346adc5a8e04302be909
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646626"
---
# <a name="system-versioned-temporal-tables-with-memory-optimized-tables"></a>Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


As tabelas temporais com controle da versão do sistema para [Tabelas com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) são projetadas para fornecer uma solução econômica para cenários nos quais há a necessidade de [auditoria de dados e análise pontual](https://msdn.microsoft.com/library/mt631669.aspx) sobre os dados coletados com cargas de trabalho OLTP in-memory. Elas fornecem alta taxa de transferência transacional, simultaneidade livre de bloqueios e, ao mesmo tempo, a capacidade de armazenar grande quantidade de dados de histórico que podem ser consultados facilmente.

## <a name="overview"></a>Visão geral

As tabelas temporais com controle da versão do sistema mantêm um histórico completo de alterações de dados e expõem extensões Transact-SQL convenientes para a análise pontual. Em um cenário típico, o histórico de dados é retido por um período muito longo (vários meses, até mesmo anos), embora não seja consultado regularmente.

A auditoria de dados e a análise baseada em tempo podem ser solicitadas em ambientes diferentes, especialmente em sistemas OLTP que processam quantidades extremamente grandes de solicitações e nos quais a tecnologia de OLTP in-memory é usada. No entanto, o uso de tabelas com otimização de memória em cenários temporais é um desafio, pois uma grande quantidade de dados históricos gerados normalmente excede o limite de memória RAM disponível. Ao mesmo tempo, usar RAM para armazenar dados históricos somente leitura acessados com menos frequência à medida que envelhecem, não é uma solução ideal.

As tabelas temporais com controle da versão do sistema para tabelas com otimização de memória fornecem alta taxa de transferência transacional, simultaneidade livre de bloqueios e, ao mesmo tempo, a capacidade de armazenar uma grande quantidade de dados de histórico usando tabelas na memória para armazenar dados atuais (a tabela temporal) e tabelas baseadas em disco para dados históricos. O impacto em operações DML é minimalizado com o uso de uma tabela de preparo com otimização de memória interna gerada automaticamente que armazena o histórico recente e permite a execução de DMLs a partir do código compilado nativamente.

O diagrama a seguir ilustra essa arquitetura.![Arquitetura Temporal Na Memória](../../relational-databases/tables/media/temporal-in-memory-architecture.png "Arquitetura temporal na memória")

## <a name="implementation-details"></a>Detalhes da implementação

Os fatos a seguir sobre as tabelas temporais com controle da versão do sistema com tabelas otimizadas para memória são considerações das quais você deve estar ciente ao criar uma tabela temporal com controle da versão do sistema. Para obter opções de sintaxe e um exemplo, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).

- Apenas as tabelas com otimização de memória podem ter controle da versão do sistema (**DURABILITY = SCHEMA_AND_DATA**).
- A tabela de histórico para a tabela com controle da versão do sistema com otimização de memória deve ter base em disco, independentemente de ter sido criada pelo usuário final ou o sistema.
- Consultas que afetam apenas a tabela atual (na memória) podem ser usadas em [módulos T-SQL compilados nativamente](https://msdn.microsoft.com/library/dn133184.aspx). Não há suporte para consultas temporais usando a cláusula FOR SYSTEM TIME em módulos compilados nativamente. O uso da cláusula FOR SYSTEM TIME com tabelas com otimização de memória em consultas ad hoc e módulos não nativos tem suporte.
- Quando **SYSTEM_VERSIONING = ON**, uma tabela interna de preparo com otimização de memória é criada automaticamente para aceitar as alterações de versão do sistema mais recentes resultantes de operações de atualização e exclusão na tabela atual com otimização de memória.
- Dados da tabela interna de preparo com otimização de memória são movidos regularmente para a tabela de histórico com base em disco pela tarefa de limpeza de dados assíncrona. Esse mecanismo de limpeza de dados tem o objetivo de manter os buffers internos da memória em menos de 10% do consumo de memória de seus objetos pai. Você pode acompanhar o consumo total de memória da tabela temporal com controle da versão do sistema com otimização de memória consultando [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md) e resumindo os dados da tabela interna de preparo com otimização de memória e a tabela temporal atual.
- Você pode impor uma liberação de dados invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md).
- Quando **SYSTEM_VERSIONING = OFF** ou quando o esquema da tabela com controle da versão do sistema for modificado pela adição, remoção ou alteração de colunas, todo o conteúdo do buffer de preparo interno é movido para a tabela de histórico com base em disco.
- A consulta de dados históricos está efetivamente sob o nível de isolamento de INSTANTÂNEO e sempre retorna uma união entre o buffer de preparo na memória e a tabela com base em disco sem duplicatas.
- As operações**ALTER TABLE** que alteram o esquema da tabela internamente devem executar uma limpeza de dados, o que pode prolongar a duração da operação.

## <a name="the-internal-memory-optimized-staging-table"></a>A tabela de preparo com otimização de memória interna

A tabela de preparo com otimização de memória interna é um objeto interno criado pelo sistema para otimizar operações DML.

- O nome da tabela é gerado no seguinte formato: **Memory_Optimized_History_Table_<object_id>** em que *<object_id>* é o identificador da tabela temporal atual.
- A tabela replica o esquema da tabela temporal atual mais uma coluna BIGINT. Essa coluna adicional garante a exclusividade das linhas movidas para o buffer de histórico interno.
- A coluna adicional tem o seguinte formato de nome: **Change_ID[_<suffix>]** , em que *_\<suffix>* é adicionado, opcionalmente, caso a tabela já tenha uma coluna *Change_ID*.
- O tamanho máximo de linha para uma tabela com otimização de memória com controle da versão do sistema é reduzido em oito bytes, devido à coluna BIGINT adicional na tabela de preparo. O novo valor máximo agora é 8052 bytes.
- A tabela de preparo interna com otimização de memória não é representada no Pesquisador de Objetos do SQL Server Management Studio.
- Os metadados sobre essa tabela, bem como sua conexão com a tabela temporal atual, podem ser encontrados em [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md).

## <a name="the-data-flush-task"></a>A tarefa de limpeza de dados

A limpeza de dados é uma tarefa ativada regularmente que verifica se alguma tabela com otimização de memória atende a uma condição de memória baseada no tamanho para movimentação de dados. A movimentação de dados começa quando o consumo de memória da tabela de preparo interna atinge 8% de consumo de memória da tabela temporal atual.

A tarefa de limpeza de dados será ativada regularmente com uma agenda que varia com base na carga de trabalho existente. Com uma carga de trabalho pesada, com uma frequência a cada cinco segundos, e com uma carga de trabalho leve, com uma frequência a cada 1 minuto. Um thread é gerado para cada tabela de preparo interna com otimização de memória que precisa de limpeza.

A limpeza de dados exclui todos os registros de buffer interno de memória mais antigos do que a transação mais antiga em execução no momento para mover esses registros para a tabela de histórico com base em disco.

Você pode impor uma limpeza de dados invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) e especificando o nome do esquema e da tabela: **sys.sp_xtp_flush_temporal_history @schema_name, @object_name** . Com este comando executado pelo usuário, o mesmo processo de movimentação de dados é invocado quando a tarefa de limpeza de dados é invocada pelo sistema na agenda interna.

## <a name="see-also"></a>Consulte Também

- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Introdução a tabelas temporais com controle da versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Cenários de uso da tabela temporal](../../relational-databases/tables/temporal-table-usage-scenarios.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Particionamento com tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
