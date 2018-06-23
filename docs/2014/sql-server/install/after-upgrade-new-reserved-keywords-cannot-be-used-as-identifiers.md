---
title: Após a atualização, palavras-chave reservadas novas não podem ser usadas como identificadores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 177c36aaeca8e6cc9d84aae21e1f99fe0bb96867
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118044"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>Depois de atualização, novas palavras-chave reservadas não poderão ser usadas como identificadores
  O Supervisor de Atualização detectou o uso de palavras que são palavras-chave reservadas. Uma palavra-chave reservada não pode ser usada como um identificador ou nome de objeto a menos que o nome seja delimitado.  
  
## <a name="component"></a>Componente  
 Mecanismo de Banco de Dados  
  
## <a name="description"></a>Description  
 No nível de compatibilidade 90 ou inferior, as seguintes palavras não são palavras-chave reservadas e podem ser usadas como identificadores ou nomes de objeto em scripts [!INCLUDE[tsql](../../includes/tsql-md.md)]. No nível de compatibilidade 100, estas palavras são palavras-chave totalmente reservadas e não devem ser usadas como identificadores ou nomes de objeto.  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>Ação corretiva  
 É recomendável renomear o objeto. Se isso não puder ser feito antes da atualização, use um dos seguintes métodos até o nome ser alterado:  
  
-   Mantenha a configuração do nível de compatibilidade do banco de dados como 90 ou inferior.  
  
-   Faça referência ao objeto usando identificadores delimitados. Por exemplo, a instrução `CREATE TABLE [MERGE] ([MERGE] int);` usa colchetes para delimitar o nome do objeto direta.  
  
## <a name="external-resources"></a>Recursos externos  
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [Identificadores delimitados (mecanismo de banco de dados)](http://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
