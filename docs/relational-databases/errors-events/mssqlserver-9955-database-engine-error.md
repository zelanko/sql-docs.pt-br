---
description: MSSQLSERVER_9955
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d58bb993cf9f4d6cac724d105bde28f9c05c77e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448690"
---
# <a name="mssqlserver_9955"></a>MSSQLSERVER_9955
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|9955|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FTXT2_MSSEARCHACCESSDENY|  
|Texto da mensagem|Falha no SQL Server ao criar o pipe nomeado '%ls' para se comunicar com o daemon de filtro de texto completo (erro do Windows: %d). Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro. Para resolver esse erro, encerre quaisquer processos do daemon de filtro de texto completo e, se necessário, reconfigure a conta de serviço iniciador de daemon de texto completo.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem é exibida porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguiu criar um pipe nomeado para se comunicar com o daemon de filtro de texto completo. Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro.  
  
## <a name="user-action"></a>Ação do usuário  
Para corrigir esse erro, encerre todos os processos do daemon de filtro de texto completo em execução e, se necessário, reconfigure a conta de host do daemon de texto completo usando o SQL Server Configuration Manager.  
  
## <a name="see-also"></a>Consulte Também  
[SQL Server Configuration Manager](~/relational-databases/sql-server-configuration-manager.md)  
[Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[Pesquisa de texto completo](~/relational-databases/search/full-text-search.md)  
  
