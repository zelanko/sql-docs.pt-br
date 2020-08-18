---
description: MSSQLSERVER_102
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d18d07aae0e07625bb75c42ce60fa5c995937e10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339372"
---
# <a name="mssqlserver_102"></a>MSSQLSERVER_102
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
  
