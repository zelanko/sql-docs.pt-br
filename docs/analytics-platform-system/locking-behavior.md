---
title: Comportamento de bloqueio
description: Saiba como o data warehouse paralelo usa o bloqueio para garantir a integridade das transações e para manter a consistência dos bancos de dados quando vários usuários estão acessando o dado ao mesmo tempo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401006"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamento de bloqueio em paralelo data warehouse
Saiba como o data warehouse paralelo usa o bloqueio para garantir a integridade das transações e para manter a consistência dos bancos de dados quando vários usuários estão acessando o dado ao mesmo tempo.  
  
## <a name="Basics"></a>Noções básicas de bloqueio  
**Modelos**  
  
O SQL Server PDW dá suporte a quatro modos de bloqueio:  
  
Exclusivo  
O bloqueio exclusivo proíbe a gravação ou leitura do objeto bloqueado até que a transação que contém o bloqueio exclusivo seja concluída. Nenhum outro bloqueio de qualquer modo é permitido enquanto o bloqueio exclusivo está em vigor. Por exemplo, DROP TABLE e CREATE DATABASE usam um bloqueio exclusivo.  
  
Compartilhado  
O bloqueio compartilhado proíbe a inicialização de um bloqueio exclusivo no objeto afetado, mas permite todos os outros modos de bloqueio. Por exemplo, a instrução SELECT inicia um bloqueio compartilhado e, portanto, permite que várias consultas acessem os dados selecionados simultaneamente, mas impede que as atualizações dos registros sejam lidas até que a instrução SELECT seja concluída.  
  
ExclusiveUpdate  
O bloqueio ExclusiveUpdate proíbe a gravação no objeto bloqueado, mas permite a leitura por meio do bloqueio compartilhado. Nenhum outro bloqueio é permitido enquanto o bloqueio ExclusiveUpdate está em vigor. Por exemplo, o banco de dados de BACKUP e o banco de dados de restauração usam um bloqueio de atualização exclusivo.  
  
SharedUpdate  
O bloqueio SharedUpdate proíbe os modos de bloqueio exclusivo e ExclusiveUpdate e permite os modos de bloqueio compartilhado e SharedUpdate no objeto. SharedUpdate modifica um objeto, mas não restringe o acesso de leitura a ele durante a modificação. Por exemplo, INSERT e UPDATE usam um bloqueio SharedUpdate.  
  
**Classes de recurso**  
  
Os bloqueios são mantidos nas seguintes classes de objetos: banco de dados, esquema, objeto (tabela, exibição ou procedimento), aplicativo (usado internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT e SCHEMARESOLUTION (um bloqueio de nível de banco de dados é obtido durante a criação, alteração ou descartando objetos de esquema ou usuários de banco de dados). Essas classes de objeto podem aparecer na coluna object_type de [Sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Comentários gerais  
Os bloqueios podem ser aplicados a bancos de dados, tabelas ou exibições.  
  
SQL Server PDW não implementa nenhum nível de isolamento configurável. Ele dá suporte ao nível de isolamento READ_UNCOMMITTED conforme definido pelo padrão ANSI. No entanto, como as operações de leitura são executadas em READ_UNCOMMITTED, poucas operações de bloqueio realmente ocorrem ou levam à contenção no sistema.  
  
SQL Server PDW se baseia no mecanismo de SQL Server subjacente para implementar o controle de bloqueio e de simultaneidade. Se as operações levam a um deadlock de SQL Server subjacente dentro do mesmo nó, SQL Server PDW aproveita o recurso de detecção de deadlock SQL Server e encerra uma das instruções de bloqueio.  
  
> [!NOTE]  
> SQL Server não permite que as instruções que estão aguardando bloqueios sejam bloqueadas por solicitações de bloqueio mais recentes. SQL Server PDW não implementou totalmente esse processo. Em SQL Server PDW, as solicitações contínuas para novos bloqueios compartilhados às vezes podem bloquear uma solicitação anterior (mas aguardando) para um bloqueio exclusivo. Por exemplo, uma instrução **Update** (exigindo um bloqueio exclusivo) pode ser bloqueada por bloqueios compartilhados que são concedidos para a série de instruções **Select** . Para resolver um processo bloqueado (identificado revisando o [Sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), pare de enviar novas solicitações até que o bloqueio exclusivo tenha sido satisfeito.  
  
## <a name="lock-definition-table"></a>Tabela de definição de bloqueio  
O SQL Server dá suporte aos seguintes tipos de bloqueios. Nem todos os tipos de bloqueio estão disponíveis no nó de controle, mas podem ocorrer em nós de computação.  
  
-   SCH-S (estabilidade do esquema). Assegura que um elemento de esquema, como uma tabela ou índice, não seja cancelado enquanto qualquer sessão mantém o bloqueio de estabilidade do esquema no elemento do esquema.  
  
-   SCH-M (modificação de esquema). Deve ser mantido por qualquer sessão que desejar alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.  
  
-   S (compartilhado). A sessão mantenedora possui acesso compartilhado ao recurso.  
  
-   U (atualização). Indica um bloqueio de atualização adquirido em recursos que podem ser atualizados eventualmente. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial no futuro.  
  
-   X (exclusivo). A sessão mantenedora possui acesso exclusivo ao recurso.  
  
-   É (de tentativa compartilhada). Indica a intenção de colocar bloqueios S em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IU (atualização de intenção). Indica a intenção de colocar bloqueios U em algum recurso subordinado na hierarquia de bloqueio.  
  
-   IX (exclusivo da tentativa). Indica a intenção de colocar bloqueios X em algum recurso subordinado na hierarquia de bloqueio.  
  
-   SIU (atualização de tentativa compartilhada). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.  
  
-   SEIS (exclusivo da intenção compartilhada). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   UIX (atualização exclusiva da tentativa). Indica a manutenção de um bloqueio de atualização de um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.  
  
-   Unidades. Usado por operações em massa.  
  
-   RangeS_S (intervalo de chaves compartilhado e bloqueio de recurso compartilhado). Indica varredura de intervalo serializável.  
  
-   RangeS_U (intervalo de chaves compartilhado e o bloqueio de recurso de atualização). Indica verificação de atualização serializável.  
  
-   RangeI_N (inserir intervalo de chaves e bloqueio de recurso nulo). Usado para testar intervalos antes de inserir uma nova chave em um índice.  
  
-   RangeI_S. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e S.  
  
-   RangeI_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e U.  
  
-   RangeI_X. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e X.  
  
-   RangeX_S. Bloqueio de conversão de intervalo de chaves criado por uma sobreposição de bloqueios RangeI_N e RangeS-S.  
  
-   RangeX_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e RangeS_U.  
  
-   RangeX_X (intervalo de chaves exclusivo e bloqueio de recurso exclusivo). Este é um bloqueio de conversão usado na atualização de uma chave em um intervalo.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
