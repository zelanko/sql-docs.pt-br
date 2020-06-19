---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac4f4d6c19eb58e9e1eb9b2eb71312f001aa5f6b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969856"
---
# <a name="mssqlserver_102"></a>MSSQLSERVER_102
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|102|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P_SYNTAXERR2|  
|Texto da mensagem|Sintaxe incorreta próxima a '%.*ls'.|  
  
## <a name="explanation"></a>Explicação  
 Indica um erro de sintaxe. Informações adicionais não estão disponíveis porque o erro impede o [!INCLUDE[ssDE](../../includes/ssde-md.md)] de processar a instrução.  
  
 Pode ser causado pela tentativa de criar uma chave simétrica que usa a criptografia RC4 ou RC4_128 preterido, quando fora do modo de compatibilidade 90 ou 100.  
  
## <a name="user-action"></a>Ação do usuário  
 Procure os erros de sintaxe na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se for criar uma chave simétrica usando RC4 ou RC4_128, selecione uma criptografia mais recente, como um dos algoritmos AES. (Recomendado.) Se for necessário usar RC4, use ALTER DATABASE SET COMPATIBILITY_LEVEL para definir o banco de dados com o nível de compatibilidade 90 ou 100. (Não recomendável.)  
  
  
