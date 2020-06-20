---
title: Após a atualização, novas palavras-chave reservadas não podem ser usadas como identificadores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 36f7f8cadcba5e114feee4a3c42de6f40070ce72
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045680"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>Depois de atualização, novas palavras-chave reservadas não poderão ser usadas como identificadores
  O Supervisor de Atualização detectou o uso de palavras que são palavras-chave reservadas. Uma palavra-chave reservada não pode ser usada como um identificador ou nome de objeto a menos que o nome seja delimitado.  
  
## <a name="component"></a>Componente  
 Mecanismo de Banco de Dados  
  
## <a name="description"></a>Descrição  
 No nível de compatibilidade 90 ou inferior, as seguintes palavras não são palavras-chave reservadas e podem ser usadas como identificadores ou nomes de objeto em scripts [!INCLUDE[tsql](../../includes/tsql-md.md)]. No nível de compatibilidade 100, estas palavras são palavras-chave totalmente reservadas e não devem ser usadas como identificadores ou nomes de objeto.  
  
-   EXTERNAL  
  
-   MESCLAR  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>Ação corretiva  
 É recomendável renomear o objeto. Se isso não puder ser feito antes da atualização, use um dos seguintes métodos até o nome ser alterado:  
  
-   Mantenha a configuração do nível de compatibilidade do banco de dados como 90 ou inferior.  
  
-   Faça referência ao objeto usando identificadores delimitados. Por exemplo, a instrução `CREATE TABLE [MERGE] ([MERGE] int);` usa colchetes para delimitar a mesclagem de nome de objeto.  
  
## <a name="external-resources"></a>Recursos externos  
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [Identificadores delimitados (Mecanismo de Banco de Dados)](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
