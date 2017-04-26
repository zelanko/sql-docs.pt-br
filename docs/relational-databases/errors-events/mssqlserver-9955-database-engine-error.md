---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c4d27af44152bb9b9816dbcdb0af7c75ea2f4db
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9955|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FTXT2_MSSEARCHACCESSDENY|  
|Texto da mensagem|Falha no SQL Server ao criar o pipe nomeado '%ls' para se comunicar com o daemon de filtro de texto completo (erro do Windows: %d). Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro. Para resolver esse erro, encerre quaisquer processos do daemon de filtro de texto completo e, se necessário, reconfigure a conta de serviço iniciador de daemon de texto completo.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem é exibida porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguiu criar um pipe nomeado para se comunicar com o daemon de filtro de texto completo. Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro.  
  
## <a name="user-action"></a>Ação do usuário  
Para corrigir esse erro, encerre todos os processos do daemon de filtro de texto completo em execução e, se necessário, reconfigure a conta de host do daemon de texto completo usando o SQL Server Configuration Manager.  
  
## <a name="see-also"></a>Consulte também  
[SQL Server Configuration Manager](~/relational-databases/sql-server-configuration-manager.md)  
[Definir a conta de serviço do Iniciador do Daemon de Filtro de Texto Completo](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[Pesquisa de Texto Completo](~/relational-databases/search/full-text-search.md)  
  

