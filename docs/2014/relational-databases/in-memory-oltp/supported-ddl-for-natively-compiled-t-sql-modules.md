---
title: Suporte a construções em procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: c54f811f2257adcb5c08f1741018be3211c1e874
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122830"
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
  
  