---
title: Janela de Saída no SSMS| Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 9e66d06d88a1febd9e1fe988a0adfd266b120221
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67683340"
---
# <a name="output-window-in-sql-server-management-studio"></a>Janela de Saída no SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
É possível abrir a Janela de Saída por meio do menu Exibir ou da combinação de teclas Ctrl+Alt+O. Há vários canais de saída disponíveis.

A tabela a seguir fornece uma visão geral dos tipos de mensagens associados a cada canal de saída.

|Canal|Descrição|
|-----------|---------------|  
|**Telemetria**|Telemetria é o fluxo de [dados de uso de recursos anônimos](sql-server-management-studio-ssms.md) coletados pela Microsoft. Esses eventos podem ser úteis para a manutenção de um registro próprio do uso do SSMS. A Telemetria pode ajudar a identificar quais nós do Pesquisador de Objetos foram expandidos e quais comandos foram executados durante uma sessão do SSMS em que a Janela de Saída estava aberta.|
|**Pesquisador de Objetos**|Como saída, esse canal fornece o texto da consulta e tempo decorrido das consultas SQL necessárias para expandir os nós no Pesquisador de Objetos. Cada consulta registra um evento Iniciar Consulta e um evento Encerrar Consulta. Cada evento tem um carimbo de data/hora e o URN associado à entidade sendo consultada. O [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx) refere-se ao SQL Management Object subjacente e consiste em uma hierarquia estilo XPath. Por exemplo, o URN de uma tabela denominada "Table1" no banco de dados "Db" no servidor "MyServer" seria "Server[@Name='MyServer']/Database[@Name='Db']/Table[/@Name='Table1']". A expansão de um nó no Pesquisador de Objetos poderia executar várias dessas consultas com parâmetros diferentes. O evento Encerrar Consulta conterá o tempo decorrido da consulta juntamente com o texto TSQL. Você poderá considerar esses dados de consulta úteis para uma análise de desempenho do servidor em casos em que o Pesquisador de Objetos estiver excepcionalmente lento para expandir um nó específico. **Observação:** nem todo nó no Pesquisador de Objetos fornece esse nível de detalhe da consulta ao expandir.|
|**Monitor de Atividade**|Esse canal é iniciado quando o [Monitor de Atividade é aberto](https://docs.microsoft.com/sql/relational-databases/performance-monitor/activity-monitor) para um servidor. Esse fluxo contém eventos que mostram parte do texto da consulta e o carimbo de data/hora de cada consulta, mensagens de erro e notificações do monitor em pausa devido a problemas de conectividade. Se o Monitor de Atividade aparentar estar ocioso ou não atualizar, verifique esse canal de saída para obter mais informações.|





