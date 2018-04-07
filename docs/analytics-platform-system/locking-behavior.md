---
title: Comportamento de bloqueio (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c55c636e-b767-4a0c-8184-be991a10801f
caps.latest.revision: 27
ms.openlocfilehash: db8b05abe5d3eea3a927cdf410e7aa8df5ed2032
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="locking-behavior"></a>Comportamento de bloqueio
PDW do SQL Server usa bloqueio para garantir a integridade de transações e para manter a consistência de bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo.  
  
## <a name="Basics"></a>Noções básicas de bloqueio  
**Modos**  
  
SQL Server PDW dá suporte a quatro modos de bloqueio:  
  
Exclusive  
O bloqueio exclusivo impede a gravação ou leitura do objeto bloqueado até que a transação mantendo que o bloqueio exclusivo é concluída. Não há outros bloqueios de qualquer modo são permitidos enquanto o bloqueio exclusivo está em vigor. Por exemplo, DROP TABLE e CREATE DATABASE usam um bloqueio exclusivo.  
  
Compartilhada  
O bloqueio compartilhado impede a inicialização de um bloqueio exclusivo no objeto afetado, mas permite que todos os outros modos de bloqueio. Por exemplo, a instrução SELECT inicia um bloqueio compartilhado e, portanto, permite que várias consultas acessar os dados selecionados ao mesmo tempo, mas impede que atualizações para os registros sendo lidos, até que a instrução SELECT seja concluída.  
  
ExclusiveUpdate  
O bloqueio de ExclusiveUpdate proíbe a gravação para o objeto bloqueado, mas permitir a leitura por meio do bloqueio compartilhado. Outros bloqueios não são permitidos enquanto o bloqueio de ExclusiveUpdate estiver em vigor. Por exemplo, o banco de dados de BACKUP e restauração do banco de dados usam um bloqueio de atualização exclusiva.  
  
SharedUpdate  
O bloqueio de SharedUpdate proíbe modos de bloqueio exclusivo e ExclusiveUpdate e permite que os modos de bloqueio compartilhado e SharedUpdate no objeto. SharedUpdate modifica um objeto, mas não restringe o acesso de leitura a ele durante a modificação. Por exemplo, INSERT e UPDATE use um bloqueio de SharedUpdate.  
  
**Classes de recursos**  
  
Bloqueios são mantidos nos seguintes classes de objetos: banco de dados, esquema, objeto (tabela, exibição ou procedimento), (usado internamente) do aplicativo, EXTERNALDATASOURCE, SCHEMARESOLUTION e de EXTERNALFILEFORMAT (um nível de banco de dados de bloqueio obtido durante a criação, alteração, ou descarte de objetos de esquema ou os usuários de banco de dados). Essas classes de objeto podem aparecer na coluna object_type de [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Comentários gerais  
Bloqueios podem ser aplicados a bancos de dados, tabelas ou exibições.  
  
SQL Server PDW não implementa os níveis de isolamento configurável. Ele dá suporte o nível de isolamento READ_UNCOMMITTED conforme definido pelo padrão ANSI. No entanto, desde que as operações são executadas em READ_UNCOMMITTED de leitura, poucas operações de bloqueio realmente ocorrerem ou levam à contenção no sistema.  
  
SQL Server PDW depende do mecanismo subjacente do SQL Server para implementar o controle de simultaneidade e bloqueio. Se operações levam a um deadlock subjacente do SQL Server no mesmo nó, o SQL Server PDW aproveita o recurso de detecção de deadlock do SQL Server e será encerrado uma das instruções de bloqueio.  
  
> [!NOTE]  
> SQL Server não permite instruções que estão aguardando bloqueios sejam bloqueadas por solicitações de bloqueio mais recentes. SQL Server PDW não totalmente implementado esse processo. No SQL Server PDW, solicitações contínuas de novos bloqueios compartilhados às vezes podem bloquear uma solicitação anterior (mas espera) para um bloqueio exclusivo. Por exemplo, um **atualização** (que exige um bloqueio exclusivo) de instrução pode ser bloqueada por bloqueios compartilhados que são concedidos para a série de **selecione** instruções. Para resolver um processo bloqueado (identificado ao examinar o [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), interrompa a enviar novas solicitações até que o bloqueio exclusivo foi atendido.  
  
## <a name="lock-definition-table"></a>Tabela de definição de bloqueio  
SQL Server suporta os seguintes tipos de bloqueios. Nem todos os tipos de bloqueio disponíveis no nó de controle, mas podem ocorrer em nós de computação.  
  
-   SCH-S (estabilidade do esquema). Assegura que um elemento de esquema, como uma tabela ou índice, não seja cancelado enquanto qualquer sessão mantém o bloqueio de estabilidade do esquema no elemento do esquema.  
  
-   SCH-M (Schema modification). Deve ser mantido por qualquer sessão que desejar alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.  
  
-   S (compartilhado). A sessão mantenedora possui acesso compartilhado ao recurso.  
  
-   U (atualização). Indica um bloqueio de atualização adquirido em recursos que podem ser atualizados eventualmente. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial no futuro.  
  
-   X (exclusivo). A sessão mantenedora possui acesso exclusivo ao recurso.  
  
-   É (intencional compartilhado). Indica a intenção de colocar bloqueios S em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IU (atualização intencional). Indica a intenção de colocar bloqueios U em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IX (exclusivo intencional). Indica a intenção de colocar bloqueios X em algum recurso subordinado na hierarquia de bloqueio.  
  
-   SIU (atualização intencional compartilhada). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.  
  
-   SEIS (exclusivo intencional de compartilhamento). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   UIX (exclusivo intencional de atualização). Indica a manutenção de um bloqueio de atualização de um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   ATUALIZAÇÃO EM MASSA. Usado por operações em massa.  
  
-   RangeS_S (intervalo de chave compartilhada e o recurso compartilhado bloqueio). Indica varredura de intervalo serializável.  
  
-   RangeS_U (intervalo de chave compartilhada e atualização de bloqueio de recurso). Indica verificação de atualização serializável.  
  
-   RangeI_N (bloqueio de intervalo de chave de inserção e de recurso nulo). Usado para testar intervalos antes de inserir uma nova chave em um índice.  
  
-   RangeI_S. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e S.  
  
-   RangeI_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e U.  
  
-   RangeI_X. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e X.  
  
-   RangeX_S. Bloqueio de conversão de intervalo de chaves criado por uma sobreposição de bloqueios RangeI_N e RangeS-S.  
  
-   RangeX_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e RangeS_U.  
  
-   RangeX_X (bloqueio de intervalo de chave exclusivo e de recurso exclusivo). Este é um bloqueio de conversão usado na atualização de uma chave em um intervalo.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
