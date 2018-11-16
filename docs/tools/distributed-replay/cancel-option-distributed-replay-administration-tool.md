---
title: Opção de cancelamento (ferramenta de administração do Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 93aa54bc208980b495aac1b2b33fe11e3472d50e
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291062"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>Opção de cancelamento (ferramenta de administração do Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A ferramenta de administração [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, é uma ferramenta de linha de comando que você pode usar para se comunicar com o controlador de reprodução distribuída. Este tópico descreve a opção de linha de comando **cancel** e a sintaxe correspondente.  
  
 A opção **cancel** cancela a operação atual que está em execução no controlador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dreplay cancel [-m controller] [-q]   
```  
  
#### <a name="parameters"></a>Parâmetros  
 **-m** *controller*  
 O nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.  
  
 Se o parâmetro **-m** não for especificado, será usado o computador local.  
  
 **-q**  
 Modo silencioso. Não solicita confirmação.  
  
 O parâmetro **-q** é opcional.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, uma solicitação de cancelamento é enviada no modo silencioso. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração.  
  
```  
dreplay cancel –m localhost -q  
```  
  
## <a name="permissions"></a>Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
