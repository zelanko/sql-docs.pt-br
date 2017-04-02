---
title: "Formatos de dados para importar ou exportar em massa (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "formatos de dados [SQL Server], escolhendo"
  - "importação em massa [SQL Server], formatos de dados"
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
caps.latest.revision: 29
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 29
---
# Formatos de dados para importar ou exportar em massa (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode aceitar dados em formato de dados de caractere ou formato de dados binário nativos. Use o formato de caractere ao mover dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outro aplicativo (como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) ou outro servidor de banco de dados (como Oracle ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). O formato nativo só pode ser usado para transferir dados entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Neste tópico:**  
  
-   [Formatos de dados para importar ou exportar em massa](#ComponentsAndConcepts)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Formatos de dados para importar ou exportar em massa  
 A tabela a seguir indica o formato de dados que costuma ser adequado ao uso, dependendo de como os dados estão representados e da origem ou destino da operação.  
  
|Operação|Nativo|Unicode nativo|Caractere|Caractere unicode|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum caractere estendido ou DBCS (conjunto de caracteres de dois bytes). A menos que um arquivo de formato seja usado, essas tabelas devem ser definidas identicamente.|Sim*|—|—|—|  
|Para colunas **sql_variant**, recomenda-se usar o formato de dados nativos que, ao contrário dos formatos Unicode e de caractere, preservam os metadados de cada valor **sql_variant**.|Sim|—|—|—|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que contém caracteres estendidos ou DBCS.|—|Sim|—|—|  
|Importação de dados em massa de um arquivo de texto gerado por outro programa.|—|—|Sim|—|  
|Exportação de dados em massa para um arquivo de texto que será usado em outro programa.|—|—|Sim|—|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que contém dados unicode e não contém nenhum caractere estendido ou DBCS.|—|—|—|Sim|  
  
 \* Método mais rápido para a exportação de dados em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao usar **bcp**.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  