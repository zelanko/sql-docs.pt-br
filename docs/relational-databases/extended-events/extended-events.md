---
title: Visão geral de XEvents – SQL Server
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
- XEvents
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 34ebcae99f096d095839cb533fb6efe58b113050
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75234597"
---
# <a name="extended-events-overview"></a>Visão geral de eventos estendidos

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A arquitetura de eventos estendidos permite que os usuários coletem um volume de dados tão grande ou tão pequeno quanto necessário para identificar ou solucionar um problema de desempenho. Os Eventos Estendidos são configuráveis e escalam muito bem.

Você pode encontrar mais informações sobre Eventos Estendidos em [Início Rápido: eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md).

## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Benefícios de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

Os Eventos Estendidos são um sistema de monitoramento de desempenho de peso leve que usa o mínimo possível de recursos de desempenho. Os Eventos Estendidos fornecem duas interfaces gráficas do usuário para criar, modificar, exibir e analisar os dados da sessão. Essas interfaces são nomeadas:

- Assistente para Nova Sessão
- Nova Sessão

## <a name="extended-events-concepts"></a>Conceitos de eventos estendidos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os Eventos Estendidos são criados com base em conceitos existentes, como um evento ou um consumidor do evento, usam conceitos de Rastreamento de Eventos para Windows e apresentam novos conceitos.  
  
 A tabela a seguir descreve os conceitos em Eventos Estendidos.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Pacotes de eventos estendidos do SQL Server](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|Descreve os pacotes de Eventos Estendidos que contêm objetos. Esses objetos são usados para obter e processar dados quando uma sessão de Eventos Estendidos está em execução.|  
|[Destinos de eventos estendidos do SQL Server](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|Descreve os consumidores de evento que podem receber dados durante uma sessão de evento.|  
|[Mecanismo de eventos estendidos do SQL Server](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|Descreve o mecanismo que implementa e gerencia uma sessão de Eventos Estendidos.|  
|[Sessões de eventos estendidos do SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|Descreve a sessão de Eventos Estendidos.|  
| &nbsp; | &nbsp; |
  
## <a name="extended-events-architecture"></a>Arquitetura de eventos estendidos  

Os Eventos Estendidos são o nome que usamos para um sistema geral de manipulação de eventos para sistemas de servidores. A infraestrutura de Eventos Estendidos oferece suporte à correlação de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em certas condições, à correlação de dados entre sistema operacional e aplicativos de banco de dados. No caso do sistema operacional, a saída de Eventos Estendidos deve ser direcionada para o ETW (Rastreamento de Eventos para Windows). O ETW ainda pode correlacionar os dados de eventos com o sistema operacional ou os dados de eventos de aplicativos.  

Todos os aplicativos têm pontos de execução que são úteis dentro e fora de um aplicativo. Dentro do aplicativo, o processamento assíncrono pode ser enfileirado usando informações coletadas durante a execução inicial de uma tarefa. Fora do aplicativo, os pontos de execução fornecem informações aos utilitários de monitoramento. As informações são sobre as características de comportamento e de desempenho do aplicativo monitorado.  

 O sistema Eventos Estendidos oferece suporte a dados de evento fora de um processo. Esses dados são geralmente usados por:  
  
-   Ferramentas de rastreamento, como o Rastreamento do SQL e o Monitor do Sistema.  
  
-   Ferramentas de log, como o log de eventos do Windows ou o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usuários que administram um produto ou desenvolvem aplicativos em um produto.  
  
 Os Eventos Estendidos têm os estes aspectos de design principais:  
  
-   O mecanismo Eventos Estendidos é agnóstico. Já que não é restrito ao conteúdo do evento, o mecanismo pode associar qualquer evento a qualquer destino. Para obter mais informações sobre o mecanismo Eventos Estendidos, consulte [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md).  
  
-   Os eventos são separados dos consumidores de evento, que são chamados *destinos* em Eventos Estendidos. Isso significa que qualquer destino pode receber qualquer evento. Além disso, qualquer evento gerado pode ser consumido automaticamente pelo destino, que pode registrar em log ou fornecer contexto de evento adicional. Para obter mais informações, consulte [SQL Server Extended Events Targets](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
-   Os eventos são distintos quanto à ação quando ocorre um evento. Portanto, qualquer ação pode ser associada a qualquer evento.  
  
-   Os predicados podem filtrar dinamicamente quando os dados de evento devem ser capturados. A filtragem dinâmica confere flexibilidade à infraestrutura de Eventos Estendidos. Para obter mais informações, consulte [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 O mecanismo Eventos Estendidos pode gerar dados de evento de forma síncrona (e processar os dados de forma assíncrona) o que fornece uma solução flexível para manipulação de eventos. Além disso, o mecanismo Eventos Estendidos fornece os seguintes recursos:  
  
-   Uma abordagem unificada no tratamento de eventos em todo o sistema de servidor, permitindo, ao mesmo tempo, que os usuários isolem eventos específicos com a finalidade de solucionar problemas.  
  
-   Integração com e suporte às ferramentas de ETW existentes.  
  
-   Um mecanismo de tratamento de evento completamente configurável baseado no [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de monitorar processos ativos dinamicamente com efeito mínimo sobre esses processos.  
  
-   Uma sessão de integridade de sistema padrão que é executada sem efeitos de desempenho notáveis. A sessão coleta dados do sistema que você pode usar para ajudar a solucionar problemas de desempenho. Para obter mais informações, veja [Usar a sessão system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="extended-events-tasks"></a>Tarefas de eventos estendidos  

Usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] para executar instruções DDL, exibições e funções de gerenciamento dinâmico ou exibições de catálogo [!INCLUDE[tsql](../../includes/tsql-md.md)] , é possível criar soluções para problemas simples ou complexos de eventos estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para seu ambiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Use o **Pesquisador de Objetos** para gerenciar sessões de eventos.|[Gerenciar sessões de evento no Pesquisador de Objetos](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|Descreve como criar uma sessão de Eventos Estendidos.|[Criar uma sessão de Eventos Estendidos](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|Descreve como exibir e atualizar dados de destino.| [Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|Descreve como usar as ferramentas de Eventos Estendidos para criar e gerenciar suas sessões de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Ferramentas de Eventos Estendidos](../../relational-databases/extended-events/extended-events-tools.md)|  
|Descreve como alterar uma sessão de Eventos Estendidos.|[Alterar uma sessão de Eventos Estendidos](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|Descreve como obter informações sobre os campos associados aos eventos.|[Obter os campos de todos os eventos](https://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|Descreve como descobrir quais eventos estão disponíveis nos pacotes registrados.|[Exibir os eventos de pacotes registrados](https://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|Descreve como determinar quais destinos de Eventos Estendidos estão disponíveis nos pacotes registrados.|[Exibir os destinos dos Eventos Estendidos de pacotes registrados](https://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|Descreve como exibir os eventos e as ações dos Eventos Estendidos que são equivalentes a cada evento de Rastreamento do SQL e suas colunas associadas.|[Exibir os Eventos Estendidos equivalentes às classes de rastreamento de eventos do SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Descreve como localizar os parâmetros que você pode definir para o uso do argumento ADD TARGET em CREAT EVENT SESSION ou ALTER EVENT SESSION.|[Obter os parâmetros configuráveis para o argumento ADD TARGET](https://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|Descreve como converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos.|[Converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Descreve como determinar quais consultas estão mantendo o bloqueio, o plano da consulta e a pilha [!INCLUDE[tsql](../../includes/tsql-md.md)] no momento em que o bloqueio foi realizado.|[Determinar quais consultas estão mantendo bloqueios](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|Descreve como identificar a origem de bloqueios que estão obstruindo o desempenho do banco de dados.|[Localizar os objetos que detêm a maioria dos bloqueios](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Descreve como usar os Eventos Estendidos com o Rastreamento de Eventos do Windows para monitorar a atividade do sistema.|[Monitorar a atividade do sistema usando Eventos Estendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
|Usando Exibições de catálogo e DMVs (Exibições de gerenciamento dinâmico) para eventos estendidos | [SELECTs e JOINs de exibições do sistema dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |
| &nbsp; | &nbsp; |

Use a consulta T-SQL (Transact-SQL) a seguir para listar todos os eventos estendidos possíveis e suas descrições:

```sql
SELECT
     obj1.name as [XEvent-name],
     col2.name as [XEvent-column],
     obj1.description as [Descr-name],
     col2.description as [Descr-column]
  FROM
               sys.dm_xe_objects        as obj1
      JOIN sys.dm_xe_object_columns as col2 on col2.object_name = obj1.name
  ORDER BY
    obj1.name,
    col2.name
```


## <a name="code-examples-can-differ-for-azure-sql-database"></a>Os exemplos de código podem ser diferentes no Banco de Dados SQL do Azure

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>Consulte Também

[Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)  
[Suporte ao DAC para objetos e versões do SQL Server](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)  
[Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
[Monitorar aplicativos da camada de dados](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)  
&nbsp;  
[Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)  
[Exibições do catálogo de eventos estendidos (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
&nbsp;  
[XELite: Biblioteca multiplataforma para ler XEvents de arquivos XEL ou fluxos ao vivo do SQL](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/), lançado em maio de 2019.  
[Cmdlet do PowerShell de leitura SQLXEvent](https://www.powershellgallery.com/packages/SqlServer.XEvent), lançado em junho de 2019.  
[Mistérios do SQL: acompanhamento de causalidade versus sequência de eventos para sessões de XEvent (blog publicado em 1º de abril de 2019)](https://bobsql.com/sql-mysteries-causality-tracking-vs-event-sequence-for-xevent-sessions/)  
