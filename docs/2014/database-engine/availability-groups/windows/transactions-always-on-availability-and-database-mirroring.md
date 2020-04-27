---
title: Transações entre bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62813651"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn (SQL Server)
  Os [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ou o espelhamento de banco de dados não oferecem suporte a transações entre bancos de dados ou transações distribuídas. Isso é porque a atomicidade/integridade da transação não pode ser garantida pelos seguintes motivos:  
  
-   Para transações envolvendo todos os bancos de dados: cada banco de dados é confirmado de forma independente. Portanto, mesmo para bancos de dados em um único grupo de disponibilidade, um failover pode ocorrer depois que um banco de dados confirma uma transação, mas antes de o outro banco de dados confirmar. No espelhamento de banco de dados, esse problema é complexo, pois, após o failover, o banco de dados espelhado fica normalmente em uma instância de servidor diferente do outro banco de dados, e mesmo se ambos os bancos de dados forem espelhados entre os mesmos dois parceiros, não haverá garantia de que ambos os bancos de dados receberão failover ao mesmo tempo.  
  
-   Para transações distribuídas: após um failover, o novo servidor principal/réplica primária não poderá se conectar ao coordenador de transações distribuídas no servidor principal/réplica primária anterior. Portanto, o novo servidor principal/réplica primária não pode obter o status da transação.  
  
 O exemplo de espelhamento de banco de dados a seguir ilustra como uma inconsistência lógica pode ocorrer. Neste exemplo, um aplicativo usa uma transação de banco de dados cruzado para inserir duas linhas de dados: uma linha é inserida em uma tabela em um banco de dados espelho, A, e a outra linha é inserida em uma tabela em outro banco de dados, B. O banco de dados A está sendo espelhado em modo de alta segurança com failover automático. Enquanto a transação está sendo confirmada, o banco de dados A torna-se indisponível e ocorre failover automático na sessão de espelhamento para o espelho do banco de dados A.  
  
 Depois do failover, a transação entre bancos de dados pode ser confirmada com sucesso no banco de dados B, mas não no banco de dados onde ocorreu failover. Isso poderá ocorrer se o servidor original principal para o banco de dados A não enviar o log de transações entre bancos de dados para o servidor de espelho antes da falha. Depois do failover, a transação não existirá no novo servidor principal. Os bancos de dados A e B se tornarão inconsistentes, porque os dados inseridos no banco de dados B permanecerão intactos, mas os dados inseridos no banco de dados A serão perdidos.  
  
 Um cenário semelhante pode acontecer no uso de uma transação MS DTC. Por exemplo, depois do failover, o novo principal contata o MS DTC. Mas o MS DTC não tem conhecimento do novo servidor principal e encerra qualquer transação que esteja "sendo preparada para confirmação”, considerada confirmada em outros bancos de dados.  
  
> [!IMPORTANT]  
>  Usar o espelhamento de banco de dados ou grupos de disponibilidade junto com DTC não resulta em uma instalação sem suporte do SQL Server. Se, no entanto, um banco de dados faz parte de uma sessão de espelhamento de banco de dados ou do Grupo de Disponibilidade, e DTC também é usado no banco de dados, os problemas de suporte são investigados pela Microsoft somente se não relacionadas ao uso combinado de espelhamento de banco de dados ou grupos de disponibilidade com DTC.  
  
  
