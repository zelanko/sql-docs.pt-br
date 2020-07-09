---
title: Usar o XEvent Profiler do SSMS
description: O XEvent Profiler exibe um visualizador ativo de eventos estendidos. Saiba por que usar esse criador de perfil, os principais recursos e como começar a ver eventos estendidos.
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 9cd63ae6c84ce09b70246aae91c16446017f6cfc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756822"
---
# <a name="use-the-ssms-xevent-profiler"></a>Usar o XEvent Profiler do SSMS

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O XEvent Profiler do SSMS é um recurso do SSMS (SQL Server Management Studio) que exibe uma janela do visualizador dinâmico de eventos estendidos. Esta visão geral descreve os motivos para usar esse criador de perfil, os principais recursos e as instruções para começar a exibir eventos estendidos.

## <a name="why-would-i-use-the-xevent-profiler"></a>Por que usar o XEvent Profiler?
Ao contrário do SQL Profiler, o XEvent Profiler é integrado diretamente ao SSMS e criado com base na tecnologia de Eventos Estendidos escalonáveis no mecanismo do SQL. Esse recurso permite acesso rápido a uma exibição de transmissão ao vivo de eventos de diagnóstico no SQL Server. Essa exibição pode ser personalizada e as personalizações podem ser compartilhadas com outros usuários do SSMS como um arquivo .viewsettings. A sessão criada pelo XE Profiler é menos intrusiva para o SQL Server em execução do que ocorreria com um rastreamento SQL semelhante ao usar o SQL Profiler. Essa sessão também pode ser personalizada pelo usuário usando a interface do usuário existente das propriedades da sessão do XE ou pelo T-SQL.

## <a name="prerequisites"></a>Pré-requisitos
Esse recurso só está disponível no SSMS (SQL Server Management Studio) v17.3 ou posterior. Verifique se você está usando a versão mais recente. É possível encontrar a versão mais recente [aqui.](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="getting-started"></a><a id="getting-started"></a>Introdução
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
  
  
