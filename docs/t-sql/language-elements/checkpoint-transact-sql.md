---
title: CHECKPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2c7232d1494ad48987d91ffe4dfc05e5ef47e4b5
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um ponto de verificação manual no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está conectado no momento.  
  
> [!NOTE]  
>  Para obter informações sobre os diferentes tipos de pontos de verificação de banco de dados e sobre a operação de ponto de verificação em geral, confira [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *checkpoint_duration*  
 Especifica a quantidade de tempo solicitada, em segundos, para conclusão do ponto de verificação manual. Quando *checkpoint_duration* for especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tentará executar o ponto de verificação dentro da duração solicitada. *checkpoint_duration* precisa ser uma expressão do tipo **int** e precisa ser maior que zero. Quando esse parâmetro é omitido, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ajusta a duração do ponto de verificação para minimizar o impacto no desempenho em aplicativos de banco de dados. *checkpoint_duration* é uma opção avançada.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>Fatores que afetam a duração de operações do ponto de verificação  
 Em geral, o tempo necessário para uma operação de ponto de verificação aumenta conforme o número de páginas sujas que a operação deve gravar. Por padrão, para minimizar o impacto no desempenho em outros aplicativos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta a frequência de gravações executadas por uma operação de ponto de verificação. Diminuir a frequência de gravação aumenta o tempo que a operação de ponto de verificação exige para ser concluída. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará essa estratégia para um ponto de verificação manual, a não ser que um valor de *checkpoint_duration* seja especificado no comando CHECKPOINT.  
  
 O impacto do uso de *checkpoint_duration* no desempenho depende do número de páginas sujas, da atividade no sistema e da duração atual especificada. Por exemplo, se o ponto de verificação normalmente é concluído em 120 segundos, especificar um *checkpoint_duration* de 45 segundos fará com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dedique mais recursos ao ponto de verificação do que a quantidade que seria atribuída por padrão. Por outro lado, especificar um *checkpoint_duration* de 180 segundos fará com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribua menos recursos do que a quantidade que seria atribuída por padrão. Em geral, um *checkpoint_duration* curto aumentará os recursos dedicados ao ponto de verificação, enquanto um *checkpoint_duration* longo reduzirá os recursos dedicados ao ponto de verificação. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre conclui um ponto de verificação, se possível, e a instrução CHECKPOINT retorna imediatamente quando um ponto de verificação é concluído. Então, em alguns casos, um ponto de verificação pode ser concluído antes da duração especificada ou pode ser executado por mais tempo que a duração especificada.  
  
##  <a name="Security"></a> Segurança  
  
### <a name="permissions"></a>Permissões  
 As permissões de CHECKPOINT são o padrão para os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_backupoperator** e não podem ser transferidas.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Configurar a opção de configuração do servidor do intervalo de recuperação](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
