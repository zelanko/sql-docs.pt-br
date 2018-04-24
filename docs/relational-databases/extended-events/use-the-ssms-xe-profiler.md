---
title: Usar o XEvent Profiler do SSMS | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: genemi
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5d168a388308ca769591e615de32689ce9e92a5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="use-the-ssms-xevent-profiler"></a>Usar o XEvent Profiler do SSMS
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
O XEvent Profiler do SSMS é um recurso do SSMS (SQL Server Management Studio) que exibe uma janela do visualizador dinâmico de eventos estendidos. Esta visão geral descreve os motivos para usar esse criador de perfil, os principais recursos e as instruções para começar a exibir eventos estendidos.

## <a name="why-would-i-use-the-xevent-profiler"></a>Por que usar o XEvent Profiler?
Ao contrário do SQL Profiler, o XEvent Profiler é integrado diretamente ao SSMS e criado com base na tecnologia de Eventos Estendidos escalonáveis no mecanismo do SQL. Esse recurso permite acesso rápido a uma exibição de transmissão ao vivo de eventos de diagnóstico no SQL Server. Essa exibição pode ser personalizada e as personalizações podem ser compartilhadas com outros usuários do SSMS como um arquivo .viewsettings. A sessão criada pelo XE Profiler é menos intrusiva para o SQL Server em execução do que ocorreria com um rastreamento SQL semelhante ao usar o SQL Profiler. Essa sessão também pode ser personalizada pelo usuário usando a interface do usuário existente das propriedades da sessão do XE ou pelo T-SQL.

## <a name="prerequisites"></a>Prerequisites
Esse recurso só está disponível no SSMS (SQL Server Management Studio) v17.3 ou posterior. Verifique se você está usando a versão mais recente. É possível encontrar a versão mais recente [aqui.](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)

## <a id="getting-started"></a>Introdução
Para acessar o XEvent Profiler, siga estas etapas:

1. Abra o **SQL Server Management Studio**.

2. Conecte-se a uma instância do Mecanismo de Banco de Dados do Microsoft SQL Server ou do localhost.

3. No Pesquisador de Objetos, encontre o item de menu XE Profiler e expanda-o clicando no sinal "+".

   ![Menu do XE Profiler](media/xevents-xe-profiler-menu.png)

4. Clique duas vezes em **Padrão** se desejar exibir todos os eventos estendidos nesta sessão. Clique em **T-SQL** se desejar exibir as instruções SQL registradas. Uma sessão será criada para você caso isso ainda não tenha ocorrido.

   ![Sessão do XE Profiler](media/xevents-xe-profiler-start-session.png)

5. Agora você pode exibir os Eventos Estendidos.

   ![Visualizador do XE Profiler](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>Consulte Também
[Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
[Ferramentas de Eventos Estendidos](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
