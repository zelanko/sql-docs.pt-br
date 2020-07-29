---
title: Opção de status na ferramenta de administração
titleSuffix: SQL Server Distributed Replay
description: Este artigo descreve a opção de linha de comando de status e a sintaxe da ferramenta de administração do SQL Server Distributed Replay, que exibe o status atual.
ms.prod: sql
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 891c66ddb9b2124bb4f7cc32ad391fe4d41d42a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732168"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opção de status (ferramenta de administração do Distributed Replay)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

A ferramenta de administração [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, é uma ferramenta de linha de comando que você pode usar para se comunicar com o controlador de reprodução distribuída. Este tópico descreve a opção de linha de comando **status** e a sintaxe correspondente.  
  
 A opção **status** consulta o controlador e exibe o status atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 **-m** _controlador_  
 Especifica o nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.  
  
 Se o parâmetro **-m** não for especificado, será usado o computador local.  
  
 **-f** _intervalo_de_status_  
 Especifica a frequência (em segundos) na qual exibir o status.  
  
 Se o parâmetro **-f** não for especificado, o intervalo padrão será de 30 segundos.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o status atual é exibido a cada 60 segundos. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração.  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
