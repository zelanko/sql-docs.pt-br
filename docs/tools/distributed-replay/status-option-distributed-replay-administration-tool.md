---
title: "Op&#231;&#227;o de status (ferramenta de administra&#231;&#227;o do Distributed Replay) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# Op&#231;&#227;o de status (ferramenta de administra&#231;&#227;o do Distributed Replay)
  A ferramenta de administração [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, é uma ferramenta de linha de comando que você pode usar para se comunicar com o controlador de reprodução distribuída. Este tópico descreve a opção de linha de comando **status** e a sintaxe correspondente.  
  
 A opção **status** consulta o controlador e exibe o status atual.  
  
 ![Ícone de vínculo de tópico](../../database-engine/configure-windows/media/topic-link.png "Ícone de vínculo de tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, consulte [Convenções de sintaxe do Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## Sintaxe  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### Parâmetros  
 **-m** *controller*  
 Especifica o nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.  
  
 Se o parâmetro **-m** não for especificado, será usado o computador local.  
  
 **-f** *status_interval*  
 Especifica a frequência (em segundos) na qual exibir o status.  
  
 Se o parâmetro **-f** não for especificado, o intervalo padrão será de 30 segundos.  
  
## Exemplos  
 No exemplo a seguir, o status atual é exibido a cada 60 segundos. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração.  
  
```  
dreplay status –m localhost -f 60  
```  
  
## Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## Consulte também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  