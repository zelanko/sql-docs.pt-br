---
title: Objetos do sistema relacionados ao XEvents
description: Esses recursos estão relacionados a eventos estendidos, incluindo como os objetos do sistema dão suporte a eles, como p SQL Server os utiliza e aspectos específicos do Banco de Dados SQL do Azure.
ms.date: 03/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jukoesma
ms.technology: xevents
ms.topic: reference
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2db8a1ca2d96046c9eb3d3d5e8dd393b0342334d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79487564"
---
# <a name="system-objects-that-support-extended-events"></a>Objetos do sistema que suportam eventos estendidos

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O presente artigo fornece links para outros artigos relacionados a eventos estendidos. São artigos que descrevem o seguinte:

- Objetos do sistema que dão suporte ao recurso de eventos estendidos.
- Partes do próprio SQL Server que usam eventos estendidos.
- Aspectos de eventos estendidos que são específicos do Banco de Dados SQL do Azure na nuvem.

As listas não estão necessariamente completas.

## <a name="system-tables"></a>Tabelas do sistema

- [Tabelas de eventos estendidas – trace_xe_action_map](../system-tables/extended-events-tables-trace-xe-action-map.md)

- [Tabelas de eventos estendidas – trace_xe_event_map](../system-tables/extended-events-tables-trace-xe-event-map.md)

## <a name="system-catalog-views"></a>Exibições de catálogo do sistema

- [Exibições do catálogo de eventos estendidos (Transact-SQL)](../system-catalog-views/extended-events-catalog-views-transact-sql.md)

- [sys.server_event_sessions (Transact-SQL)](../system-catalog-views/sys-server-event-sessions-transact-sql.md)

- [sys.server_event_session_actions (Transact-SQL)](../system-catalog-views/sys-server-event-session-actions-transact-sql.md)

- [sys.server_event_session_events (Transact-SQL)](../system-catalog-views/sys-server-event-session-events-transact-sql.md)

- [sys.server_event_session_fields (Transact-SQL)](../system-catalog-views/sys-server-event-session-fields-transact-sql.md)

- [sys.server_event_session_targets (Transact-SQL)](../system-catalog-views/sys-server-event-session-targets-transact-sql.md)

## <a name="other-system-objects"></a>Outros objetos do sistema

- [Exibições de gerenciamento dinâmico de eventos estendidos](../system-dynamic-management-views/extended-events-dynamic-management-views.md)

## <a name="uses-of-extended-events-by-sql-server-itself"></a>Usos de eventos estendidos pelo próprio SQL Server

Esta lista não pretende ser completa.

- [Acessar informações de diagnóstico nos logs de eventos estendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)

- [Configurar eventos estendidos para Grupos de Disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/always-on-extended-events.md)

- [Eventos estendidos para o Stretch Database](../../sql-server/stretch-database/extended-events-for-stretch-database.md)

## <a name="azure-sql-database-and-extended-events"></a>Eventos estendidos no Banco de Dados SQL do Azure

- [Eventos estendidos no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-xevent-db-diff-from-svr)

- [sys.database_event_session_targets (Banco de Dados SQL do Azure)](../system-catalog-views/sys-database-event-session-targets-azure-sql-database.md)

- [sys.database_event_session_fields (Banco de Dados SQL do Azure)](../system-catalog-views/sys-database-event-session-fields-azure-sql-database.md)

- [sys.database_event_session_events (Banco de Dados SQL do Azure)](../system-catalog-views/sys-database-event-session-events-azure-sql-database.md)

- [sys.database_event_session_actions (Banco de Dados SQL do Azure)](../system-catalog-views/sys-database-event-session-actions-azure-sql-database.md)
