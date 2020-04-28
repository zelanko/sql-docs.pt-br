---
title: sys. dm_db_xtp_gc_cycle_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_gc_cycle_stats_TSQL
- dm_db_xtp_gc_cycle_stats
- sys.dm_db_xtp_gc_cycle_stats_TSQL
- sys.dm_db_xtp_gc_cycle_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_gc_cycle_stats dynamic management view
ms.assetid: bbc9704e-158e-4d32-b693-f00dce31cd2f
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 95e173cd20bd04c3b5a5a6cd7ad7299ef13971d3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68026854"
---
# <a name="sysdm_db_xtp_gc_cycle_stats-transact-sql"></a>sys.dm_db_xtp_gc_cycle_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Envia o estado atual das transações confirmadas que excluíram uma ou mais linhas. O thread inativo de coleta de lixo é ativado a cada minuto ou quando o número de transações DML confirmadas excede um limite interno desde o último ciclo de coleta de lixo. Como parte do ciclo de coleta de lixo, ele move as transações que foram confirmadas em uma ou mais filas associadas às gerações. As transações que geraram versões obsoletas são agrupadas em uma unidade de 16 transações em 16 gerações, da seguinte maneira:  
  
-   Geração 0: armazena todas as transações confirmadas antes da transação ativa mais antiga. As versões de linha geradas por essas transações são imediatamente disponibilizadas para coleta de lixo.  
  
-   Gerações 1 a 14: armazena as transações com carimbo de data/hora posterior à transação ativa mais antiga. As versões de linha não podem ser coletadas como lixo. Cada geração pode reter até 16 transações. Pode existir um total de 224 (14 * 16) transações nessas gerações.  
  
-   Geração 15: as transações restantes com carimbo de data/hora posterior à transação ativa mais antiga vai para a geração 15. Similar à geração 0, não há limite de número de transações na geração 15.  
  
 Quando há pressão de memória, o thread de coleta de lixo atualiza agressivamente a dica de transação ativa mais antiga, o que força a coleta de lixo.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|cycle_id|**bigint**|Um identificador de exclusividade para o ciclo de coleta de lixo.|  
|ticks_at_cycle_start|**bigint**|Tiques no momento em que o ciclo foi iniciado.|  
|ticks_at_cycle_end|**bigint**|Tiques no momento em que o ciclo foi encerrado.|  
|base_generation|**bigint**|O valor base atual da geração no banco de dados. Isso representa o carimbo de data/hora da transação ativa mais antiga usado para identificar transações de coleta de lixo. A ID da transação ativa mais antiga é atualizada no incremento 16. Por exemplo, se você tiver IDs de transação como 124, 125, 126... 139, o valor será 124. Quando você adicionar outra transação, por exemplo, 140, o valor será 140.|  
|xacts_copied_to_local|**bigint**|O número de transações copiadas de pipeline da transação na matriz de geração de banco de dados.|  
|xacts_in_gen_0- xacts_in_gen_15|**bigint**|Número de transações em cada geração.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="usage-scenario"></a>Cenário de uso  
 Aqui está uma saída de exemplo com um subconjunto de colunas, mostrando 27 gerações:  
  
```  
cycle_id   ticks_at_cycle_start ticks_at_cycle_end   base_generation  xacts_in_gen_0    xacts_in_gen_1  
  
1          123160509            123160509            1                    0                    0  
2          123176822            123176822            1                    0                    1  
3          123236826            123236826            1                    0                    1  
4          123296829            123296829            1                    0                    1  
5          123356832            123356941            129                  0                    0  
6          123357473            123357473            129                  0                    0  
7          123417486            123417486            129                  0                    0  
8          123477489            123477489            129                  0                    0  
9          123537492            123537492            129                  0                    0  
10         123597500            123597500            129                  0                    0  
11         123657504            123657504            129                  0                    0  
12         123717507            123717507            129                  0                    0  
13         123777510            123777510            129                  0                    0  
14         123837513            123837513            129                  0                    0  
15         123897516            123897516            129                  0                    0  
16         123957516            123957516            129                  0                    0  
17         124017516            124017516            129                  0                    0  
18         124077517            124077517            129                  0                    0  
19         124137517            124137517            129                  0                    0  
20         124197518            124197518            129                  0                    0  
21         124257518            124257518            129                  0                    0  
22         124317523            124317523            129                  0                    0  
23         124377526            124377526            129                  0                    0  
24         124437529            124437529            129                  0                    0  
25         124497533            124497533            129                  0                    0  
26         124557536            124557536            129                  0                    0  
27         124617539            124617539            129                  0                    0  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
