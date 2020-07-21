---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9713e90fa15683fe4af619c66c9714c18c405cd5
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553001"
---
# <a name="mssqlserver_9955"></a>MSSQLSERVER_9955
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
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
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)   
 [Definir a conta de serviço para o iniciador do daemon de filtro de texto completo](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Pesquisa de texto completo](../search/full-text-search.md)  
  
  
