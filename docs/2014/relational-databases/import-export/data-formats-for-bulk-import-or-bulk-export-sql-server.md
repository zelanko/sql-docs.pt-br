---
title: Formatos de dados para importar ou exportar em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43cb42cffba31f20b0e9717204f5475b5bb156d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012083"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>Formatos de dados para importar ou exportar em massa (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode aceitar dados em formato de dados de caractere ou formato de dados binário nativos. Use o formato de caractere ao mover dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outro aplicativo (como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) ou outro servidor de banco de dados (como Oracle ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). O formato nativo só pode ser usado para transferir dados entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Neste tópico:**  
  
-   [Formatos de dados para importar ou exportar em massa](#ComponentsAndConcepts)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="data-formats-for-bulk-import-or-export"></a><a name="ComponentsAndConcepts"></a> Formatos de dados para importar ou exportar em massa  
 A tabela a seguir indica o formato de dados que costuma ser adequado ao uso, dependendo de como os dados estão representados e da origem ou destino da operação.  
  
|Operação|Nativo|Unicode nativo|Caractere|Caractere unicode|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum caractere estendido ou DBCS (conjunto de caracteres de dois bytes). A menos que um arquivo de formato seja usado, essas tabelas devem ser definidas identicamente.|Sim<sup>1</sup>|-|-|-|  
|Para colunas `sql_variant`, recomenda-se usar o formato de dados nativos que, ao contrário dos formatos unicode e de caractere, preservam o metadados para cada valor `sql_variant`.|Sim|-|-|-|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que contém caracteres estendidos ou DBCS.|-|Sim|-|-|  
|Importação de dados em massa de um arquivo de texto gerado por outro programa.|-|-|Sim|-|  
|Exportação de dados em massa para um arquivo de texto que será usado em outro programa.|-|-|Sim|-|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que contém dados unicode e não contém nenhum caractere estendido ou DBCS.|-|-|-|Sim|  
  
 <sup>1</sup> método mais rápido para a exportação de dados em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do ao usar o **bcp**.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
