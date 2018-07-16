---
title: Suporte para construções em procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6cdd5c7d154f1841aa5c90e110a596d8684a535
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233266"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>Construções com suporte em procedimentos armazenados compilados de modo nativo
  Este tópico lista as construções com suporte nos procedimentos armazenados compilados nativamente.  
  
 Para obter informações sobre construções sem suporte, veja [Construções do Transact-SQL sem suporte pelo OLTP in-memory](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="procedure-ddl"></a>DDL do procedimento  
 Há suporte para o seguinte:  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (necessário para procedimentos armazenados compilados nativamente)  
  
-   NATIVE_COMPILATION  
  
-   Os parâmetros podem ser declarados com NOT NULL.  
  
-   Parâmetros com valor de tabela.  
  
## <a name="security"></a>Segurança  
 Há suporte para o seguinte:  
  
-   Para procedimentos: EXECUTE AS OWNER, SELF e usuário.  
  
-   Permissões GRANT e DENY em tabelas e procedimentos.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  
