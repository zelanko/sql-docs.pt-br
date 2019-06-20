---
title: Comportamento de bloqueio – Parallel Data Warehouse | Microsoft Docs
description: Saiba como Parallel Data Warehouse usa bloqueio para garantir a integridade de transações e manter a consistência dos bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f9862fed432036dcb4a3905fb3af1d3132349a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280888"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamento de bloqueio no Parallel Data Warehouse
Saiba como Parallel Data Warehouse usa bloqueio para garantir a integridade de transações e manter a consistência dos bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo.  
  
## <a name="Basics"></a>Noções básicas de bloqueio  
**Modos**  
  
PDW do SQL Server dá suporte a quatro modos de bloqueio:  
  
Exclusive  
O bloqueio exclusivo impede a gravar ou ler a partir do objeto bloqueado até que a transação que contém que o bloqueio exclusivo é concluída. Não há outros bloqueios de qualquer modo são permitidos enquanto o bloqueio exclusivo estiver em vigor. Por exemplo, DROP TABLE e CREATE DATABASE usam um bloqueio exclusivo.  
  
Compartilhado  
O bloqueio compartilhado impede a inicialização de um bloqueio exclusivo no objeto afetado, mas permite que todos os outros modos de bloqueio. Por exemplo, a instrução SELECT inicia um bloqueio compartilhado e, portanto, permite que várias consultas acessar os dados selecionados ao mesmo tempo, mas impede que atualizações para os registros que estão sendo lidos, até que a instrução SELECT seja concluída.  
  
ExclusiveUpdate  
O bloqueio ExclusiveUpdate proíbe a gravação para o objeto bloqueado, mas permitir a leitura por meio do bloqueio compartilhado. Outros bloqueios não são permitidos enquanto o bloqueio ExclusiveUpdate estiver em vigor. Por exemplo, o banco de dados de BACKUP e RESTAURAR o banco de dados usam um bloqueio de atualização exclusiva.  
  
SharedUpdate  
O bloqueio de SharedUpdate proíbe os modos de bloqueio exclusivo e ExclusiveUpdate e permite que os modos de bloqueio compartilhado e SharedUpdate no objeto. SharedUpdate modifica um objeto, mas não restringe o acesso de leitura a ele durante a modificação. Por exemplo, INSERT e UPDATE usar um bloqueio de SharedUpdate.  
  
**Classes de recursos**  
  
Bloqueios são mantidos nas seguintes classes de objetos: Banco de dados, esquema, a objeto (uma tabela, exibição ou procedimento), o aplicativo (usado internamente), a EXTERNALDATASOURCE, EXTERNALFILEFORMAT e SCHEMARESOLUTION (um banco de dados nível bloqueio tomado durante a criação, alterando ou removendo objetos de esquema ou os usuários de banco de dados). Essas classes de objeto podem aparecer na coluna de object_type [DM pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Comentários gerais  
Bloqueios podem ser aplicados a bancos de dados, tabelas ou exibições.  
  
SQL Server PDW não implementa quaisquer níveis de isolamento configurável. Ele suporta o nível de isolamento READ_UNCOMMITTED conforme definido pelo padrão ANSI. No entanto, desde a leitura de operações são executadas sob READ_UNCOMMITTED, poucas operações de bloqueio, na verdade, ocorrerem ou levam a contenção no sistema.  
  
SQL Server PDW se baseia no mecanismo do SQL Server subjacente para implementar o controle de simultaneidade e bloqueio. Se operações levam a um deadlock subjacente do SQL Server dentro do mesmo nó, o SQL Server PDW aproveita a capacidade de detecção de deadlock do SQL Server e encerra uma das instruções de bloqueio.  
  
> [!NOTE]  
> SQL Server não permite declarações que estão aguardando bloqueios sejam bloqueadas por solicitações de bloqueio mais recentes. SQL Server PDW não totalmente implementado esse processo. Solicitações contínuas para novos bloqueios compartilhados do SQL Server PDW, às vezes, podem bloquear a uma solicitação anterior (mas aguardando) para um bloqueio exclusivo. Por exemplo, um **atualização** instrução (que exige um bloqueio exclusivo) pode ser bloqueada por bloqueios compartilhados que são concedidos para a série de **selecione** instruções. Para resolver um processo bloqueado (identificados examinando os [DM pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), pare de enviar novas solicitações até que o bloqueio exclusivo foi atendido.  
  
## <a name="lock-definition-table"></a>Tabela de definição de bloqueio  
SQL Server suporta os seguintes tipos de bloqueios. Nem todos os tipos de bloqueio estão disponíveis no nó de controle, mas pode ocorrer em nós de computação.  
  
-   SCH-S (estabilidade do esquema). Assegura que um elemento de esquema, como uma tabela ou índice, não seja cancelado enquanto qualquer sessão mantém o bloqueio de estabilidade do esquema no elemento do esquema.  
  
-   SCH-M (Schema modification). Deve ser mantido por qualquer sessão que desejar alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.  
  
-   S (compartilhado). A sessão mantenedora possui acesso compartilhado ao recurso.  
  
-   U (atualização). Indica um bloqueio de atualização adquirido em recursos que podem ser atualizados eventualmente. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial no futuro.  
  
-   X (exclusivo). A sessão mantenedora possui acesso exclusivo ao recurso.  
  
-   É (intencional compartilhado). Indica a intenção de colocar bloqueios S em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IU (atualização intencional). Indica a intenção de colocar bloqueios U em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IX (exclusivo intencional). Indica a intenção de colocar bloqueios X em algum recurso subordinado na hierarquia de bloqueio.  
  
-   SIU (atualização intencional compartilhada). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.  
  
-   SIX (exclusivo intencional de compartilhamento). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   UIX (exclusivo intencional de atualização). Indica a manutenção de um bloqueio de atualização de um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   BU. Usado por operações em massa.  
  
-   RangeS_S (intervalo de chave compartilhada e Shared bloqueio de recurso). Indica varredura de intervalo serializável.  
  
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
  
