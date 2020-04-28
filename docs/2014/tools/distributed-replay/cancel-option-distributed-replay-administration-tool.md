---
title: Opção de cancelamento (ferramenta de administração do Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce29f56d7877712dd99553968b364b1c33471c2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177318"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>Opção de cancelamento (ferramenta de administração do Distributed Replay)
  A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramenta de administração de `DReplay.exe`Distributed Replay,, é uma ferramenta de linha de comando que você pode usar para se comunicar com o Distributed Replay Controller. Este tópico descreve a opção de linha de comando **cancel** e a sintaxe correspondente.

 A opção **cancel** cancela a operação atual que está em execução no controlador.

 ![Ícone de link do tópico](../../database-engine/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).

## <a name="syntax"></a>Sintaxe

```

dreplay cancel [-mcontroller] [-q] 
```

#### <a name="parameters"></a>parâmetros
 **-m** *controlador* o nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.

 Se o parâmetro **-m** não for especificado, será usado o computador local.

 **-q** Modo silencioso. Não solicita confirmação.

 O parâmetro **-q** é opcional.

## <a name="examples"></a>Exemplos
 No exemplo a seguir, uma solicitação de cancelamento é enviada no modo silencioso. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração.

```
dreplay cancel -m localhost -q
```

## <a name="permissions"></a>Permissões
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.

 Para saber mais, confira [Distributed Replay Security](distributed-replay-security.md).

## <a name="see-also"></a>Consulte Também
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)


