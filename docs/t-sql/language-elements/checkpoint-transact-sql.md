---
description: CHECKPOINT (Transact-SQL)
title: CHECKPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
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
author: juliemsft
ms.author: jrasnick
ms.openlocfilehash: da05183ae2b331f78f9692acc6aaff66a9455092
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459382"
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Gera um ponto de verificação manual no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está conectado no momento.  
  
> [!NOTE]  
>  Para obter informações sobre os diferentes tipos de pontos de verificação de banco de dados e sobre a operação de ponto de verificação em geral, confira [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *checkpoint_duration*  
 Especifica a quantidade de tempo solicitada, em segundos, para conclusão do ponto de verificação manual. Quando *checkpoint_duration* for especificado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tentará executar o ponto de verificação dentro da duração solicitada. *checkpoint_duration* precisa ser uma expressão do tipo **int** e precisa ser maior que zero. Quando esse parâmetro é omitido, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ajusta a duração do ponto de verificação para minimizar o impacto no desempenho em aplicativos de banco de dados. *checkpoint_duration* é uma opção avançada.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>Fatores que afetam a duração de operações do ponto de verificação  
 Em geral, o tempo necessário para uma operação de ponto de verificação aumenta conforme o número de páginas sujas que a operação deve gravar. Por padrão, para minimizar o impacto no desempenho em outros aplicativos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta a frequência de gravações executadas por uma operação de ponto de verificação. Diminuir a frequência de gravação aumenta o tempo que a operação de ponto de verificação exige para ser concluída. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará essa estratégia para um ponto de verificação manual, a não ser que um valor de *checkpoint_duration* seja especificado no comando CHECKPOINT.  
  
 O impacto do uso de *checkpoint_duration* no desempenho depende do número de páginas sujas, da atividade no sistema e da duração atual especificada. Por exemplo, se o ponto de verificação normalmente é concluído em 120 segundos, especificar um *checkpoint_duration* de 45 segundos fará com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dedique mais recursos ao ponto de verificação do que a quantidade que seria atribuída por padrão. Por outro lado, especificar um *checkpoint_duration* de 180 segundos fará com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribua menos recursos do que a quantidade que seria atribuída por padrão. Em geral, um *checkpoint_duration* curto aumentará os recursos dedicados ao ponto de verificação, enquanto um *checkpoint_duration* longo reduzirá os recursos dedicados ao ponto de verificação. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre conclui um ponto de verificação, se possível, e a instrução CHECKPOINT retorna imediatamente quando um ponto de verificação é concluído. Então, em alguns casos, um ponto de verificação pode ser concluído antes da duração especificada ou pode ser executado por mais tempo que a duração especificada.  
  
##  <a name="security"></a><a name="Security"></a> Segurança  
  
### <a name="permissions"></a>Permissões  
 As permissões CHECKPOINT retornam ao padrão para os membros da função fixa de servidor **sysadmin** e da funções fixas de banco de dados **db_owner** e **db_backupoperator** e não são transferíveis.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Configurar a opção de configuração do servidor do intervalo de recuperação](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
