---
title: Estatísticas para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4a86f94a141b1f15e2bfb7e9ff3c4428f5b33707
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76909766"
---
# <a name="statistics-for-memory-optimized-tables"></a>Estatísticas para tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O otimizador de consulta usa estatísticas sobre colunas para criar planos de consulta que melhoram o desempenho das consultas. As estatísticas são coletadas de tabelas no banco de dados e armazenadas nos metadados do banco de dados.  
  
 As estatísticas são criadas automaticamente, mas também podem ser criadas manualmente. Por exemplo, as estatísticas são criadas automaticamente para colunas de chave de índice durante a criação do índice. Para obter mais informações sobre como criar estatísticas, consulte [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Geralmente, os dados de tabela são alterados com o tempo, à medida que linhas são inseridas, atualizadas e excluídas. Isso significa que as estatísticas precisam ser atualizadas periodicamente. Por padrão, as estatísticas em tabelas são atualizadas automaticamente quando o otimizador de consulta determina que elas podem estar desatualizadas.  
  
 Considerações para estatísticas em tabelas com otimização de memória:  
  
-   A partir do SQL Server 2016 e do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], há suporte para a atualização automática de estatísticas em tabelas com otimização de memória, durante o uso de um nível de compatibilidade de banco de dados de, no mínimo, 130. Veja [Nível de compatibilidade de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Se um banco de dados contiver tabelas que foram criadas anteriormente com um nível de compatibilidade mais baixo, as estatísticas precisarão ser atualizadas manualmente uma vez, para habilitar a atualização automática das estatísticas no futuro.
  
-   Para procedimentos armazenados compilados de modo nativo, os planos de execução para consultas no procedimento são otimizados quando o procedimento é compilado. Elas não são recompiladas automaticamente quando as estatísticas são atualizadas. Portanto, as tabelas devem conter um conjunto representativo de dados antes que os procedimentos sejam criados.  
  
-   Os procedimentos armazenados compilados de modo nativo podem ser recompilados manualmente usando [sp_recompile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md), e são recompilados automaticamente se o banco de dados é colocado offline e colocado online novamente, ou se há um failover de banco de dados ou uma reinicialização de servidor.  
  
## <a name="enabling-automatic-update-of-statistics-in-existing-tables"></a>Habilitando a atualização automática de estatísticas em tabelas existentes

Quando as tabelas são criadas em um banco de dados que tem o nível de compatibilidade de, no mínimo, 130, a atualização automática de estatísticas é habilitada para todas as estatísticas nessa tabela e nenhuma outra ação é necessária.

Se um banco de dados contiver tabelas com otimização de memória que foram criadas em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um nível de compatibilidade inferior a 130, as estatísticas precisarão ser atualizadas manualmente uma vez para habilitar a atualização automática no futuro.

Para habilitar a atualização automática de estatísticas em tabelas com otimização de memória que foram criadas em um nível de compatibilidade mais antigo, siga estas etapas:

1. Atualize o nível de compatibilidade do banco de dados: `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. Atualize manualmente as estatísticas das tabelas com otimização de memória. Veja abaixo um exemplo de script que executa isso.

3. Recompile manualmente os procedimentos armazenados compilados de modo nativo para se beneficiar das estatísticas atualizadas.

*Script avulso para estatísticas:* Para tabelas com otimização de memória criadas em um nível de compatibilidade inferior, é possível executar o seguinte script Transact-SQL uma vez para atualizar as estatísticas de todas as tabelas com otimização de memória e habilitar a atualização automática de estatísticas desse ponto em diante (supondo que AUTO_UPDATE_STATISTICS esteja habilitado para o banco de dados):

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```

*Verificar se a atualização automática está habilitada:* o script a seguir verifica se a atualização automática está habilitada para estatísticas em tabelas com otimização de memória. Depois de executar o script anterior, ele retornará `1` na coluna `auto-update enabled` em todos os objetos de estatística.

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## <a name="guidelines-for-deploying-tables-and-procedures"></a>Diretrizes para implantação de tabelas e procedimentos  
 Para garantir que o otimizador de consulta tem estatísticas atualizadas durante a criação de planos de consulta, implante tabelas com otimização de memória e procedimentos armazenados compilados de modo nativo que acessam essas tabelas usando estas quatro etapas:  
  
1.  Verifique se o banco de dados tem um nível de compatibilidade de, no mínimo, 130. Veja [Nível de compatibilidade de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

2.  Crie tabelas e índices. Os índices são especificados embutidos nas instruções **CREATE TABLE** .  
  
3.  Carregue dados nas tabelas.  
  
4.  Crie procedimentos armazenados que acessam as tabelas.  
  
 A criação de procedimentos armazenados compilados de modo nativo após o carregamento dos dados e a atualização das estatísticas garante que o otimizador tem estatísticas disponíveis para as tabelas com otimização de memória. Isso garantirá planos de consulta eficientes quando o procedimento for compilado.  

## <a name="see-also"></a>Consulte Também  
 [Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
