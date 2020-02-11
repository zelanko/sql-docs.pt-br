---
title: Procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e9bdc0c104b212f3c26389c1792b6b617634a12a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62714913"
---
# <a name="natively-compiled-stored-procedures"></a>procedimentos armazenados compilados nativamente
  Os procedimentos armazenados compilados nativamente são procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados no código nativo que acessam tabelas com otimização de memória. Procedimentos armazenados compilados nativamente permitem a execução eficiente de consultas e lógica de negócios no procedimento armazenado. Para obter mais detalhes sobre o processo de compilação nativo, consulte [Native Compilation of Tables and Stored Procedures](native-compilation-of-tables-and-stored-procedures.md). Para mais informações sobre a migração de procedimentos armazenados baseados em disco para procedimentos armazenados compilados de modo nativo, veja [Problemas de migração para procedimentos armazenados compilados de modo nativo](migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Uma diferença entre procedimentos armazenados interpretados (com base em disco) e procedimentos armazenados compilados nativamente é que o procedimento armazenado interpretado é criado na primeira execução enquanto que um procedimento armazenado compilado nativamente é compilado quando é criado. Com os procedimentos armazenados compilados nativamente, muitas condições de erro (estouro aritmético, conversão de tipo e algumas condições de divisão por zero) podem ser detectadas no momento da criação e causarão a falha na geração do procedimento armazenado compilado nativamente. Com os procedimentos armazenados interpretados, essas condições de erro geralmente não causarão uma falha quando o procedimento armazenado for criado, mas todas as execuções falharão.  
  
 Tópicos desta seção:  
  
-   [Criando procedimentos armazenados compilados nativamente](creating-natively-compiled-stored-procedures.md)  
  
-   [Blocos atômicos](atomic-blocks-in-native-procedures.md)  
  
-   [Construções com suporte nos procedimentos armazenados compilados de modo nativo](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Usando Try...Catch em procedimentos armazenados compilados nativamente](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [Construções com suporte em procedimentos armazenados compilados de modo nativo](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Procedimentos armazenados compilados nativamente e opções de execução Set](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Práticas recomendadas para chamar procedimentos armazenados compilados nativamente](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Monitorando o desempenho de procedimentos armazenados compilados nativamente](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Chamando procedimentos armazenados compilados nativamente em aplicativos de acesso a dados](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Memory-Optimized Tables](memory-optimized-tables.md)  
  
  
