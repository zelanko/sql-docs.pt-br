---
title: Guia do processo de limpeza de fantasma | Microsoft Docs
description: 'Saiba mais sobre o processo de limpeza de fantasma: um processo em segundo plano que exclui registros de páginas que foram marcadas para exclusão no SQL Server.'
ms.custom: ''
ms.date: 05/02/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- ghost cleanup
- ghost records
- ghost clean up process
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 557f76e3f54811581e41ad15a5270a0c1e6e4057
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859088"
---
# <a name="ghost-cleanup-process-guide"></a>Guia do processo de limpeza de fantasma

O processo de limpeza de fantasma é um processo de thread único em segundo plano que exclui registros de páginas que foram marcadas para exclusão. O artigo a seguir oferece uma visão geral desse processo.

## <a name="ghost-records"></a>Registros fantasmas

Os registros excluídos de um nível folha de uma página de índice não são removidos fisicamente da página – em vez disso, o registro é marcado como "a ser excluído", ou *fantasmas*. Isso significa que a linha continua na página, mas um bit é alterado no cabeçalho da linha para indicar que a linha é realmente um fantasma. Isso é para otimizar o desempenho durante uma operação de exclusão. Fantasmas são necessários para o bloqueio de nível de linha, mas também são necessários para o isolamento de instantâneo, em que é necessário manter as versões de linhas mais antigas.

## <a name="ghost-record-cleanup-task"></a>Tarefa de limpeza de registro fantasma

Registros marcados para exclusão, ou *fantasmas*, são limpos pelo processo de limpeza de fantasma em segundo plano. Esse processo em segundo plano será executado somente depois que a transação de exclusão for confirmada e removerá fisicamente registros fantasmas das páginas. O processo de limpeza de fantasma é executado automaticamente em um intervalo (a cada 5 segundos para o SQL Server 2012+, a cada 10 segundos para o SQL Server 2008/2008R2) e verifica se alguma página foi marcada com registros fantasmas. Se encontrar alguma, ele excluirá os registros marcados para exclusão, ou *fantasmas*, que tocam no máximo 10 páginas com cada execução.

Quando um registro for fantasma, o banco de dados será marcado como tendo entradas fantasmas, e o processo de limpeza de fantasma examinará apenas esses bancos de dados. O processo de limpeza de fantasma também marcará o banco de dados como "não tendo nenhum registro fantasma", uma vez que todos os registros fantasma foram excluídos, e ignorará esse banco de dados na próxima vez em que for executado. O processo também ignora quaisquer bancos de dados nos quais não é possível colocar um bloqueio compartilhado e tenta novamente na próxima vez em que é executado.

A consulta abaixo pode identificar quantos registros fantasma existem em um único banco de dados. 

 ```sql
 SELECT sum(ghost_record_count) total_ghost_records, db_name(database_id) 
 FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, 'SAMPLED')
 group by database_id
 order by total_ghost_records desc
```

## <a name="disable-the-ghost-cleanup"></a>Desabilitar a limpeza de fantasma

Em sistemas de alta carga com muitas exclusões, o processo de limpeza de fantasma pode gerar um problema de desempenho impedindo a manutenção de páginas no pool de buffers e a geração de E/S. Como tal, é possível desabilitar esse processo com o uso do sinalizador de rastreamento 661. Mais informações sobre isso podem ser encontradas em [Opções de ajuste para o SQL Server ao executar cargas de trabalho de alto desempenho](https://support.microsoft.com/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa). No entanto, há implicações no desempenho decorrentes da desabilitação do processo.

Desabilitar o processo de limpeza de fantasma pode fazer seu banco de dados crescer desnecessariamente e ocasionar problemas de desempenho. Como o processo de limpeza de fantasma remove registros marcados como fantasmas, desabilitar o processo deixará esses registros na página, impedindo que o SQL Server reutilize esse espaço. Isso força o SQL Server a adicionar dados a novas páginas, gerando arquivos de banco de dados sobrecarregados e pode ocasionar também [divisões da página](indexes/specify-fill-factor-for-an-index.md). As divisões da página geram problemas de desempenho ao criar planos de execução e ao realizar operações de exame. 

Como o processo de limpeza de fantasma está desabilitado, alguma medida precisa ser tomada para remover os registros fantasmas. Uma opção é executar uma recompilação de índice, que moverá os dados nas páginas. Outra opção é executar manualmente [sp_clean_db_free_space](system-stored-procedures/sp-clean-db-free-space-transact-sql.md) (para limpar todos os arquivos de dados do banco de dados) ou [sp_clean_db_file_free_space](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) (para limpar um único arquivo de dados do banco de dados), que excluirá registros fantasmas.

 >[!warning]
 > Geralmente não é recomendável desabilitar o processo de limpeza de fantasma. Isso deverá ser testado minuciosamente em um ambiente controlado antes de ser implementado permanentemente em um ambiente de produção.


## <a name="next-steps"></a>Próximas etapas  
[Desabilitando o processo de limpeza de fantasma](https://support.microsoft.com/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa)
<br>[Remover registros fantasmas de um arquivo de banco de dados único](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)
<br>[Remover registros fantasmas de todos os arquivos de dados do banco de dados](system-stored-procedures/sp-clean-db-free-space-transact-sql.md)


