---
title: Formatos de dados para importar ou exportar em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84f44eb8ff2f35942660b8fd773962f2fda8cc9c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753564"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>Formatos de dados para importar ou exportar em massa (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode aceitar dados em formato de dados de caractere ou formato de dados binário nativos. Use o formato de caractere ao mover dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outro aplicativo (como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) ou outro servidor de banco de dados (como Oracle ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). O formato nativo só pode ser usado para transferir dados entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Neste tópico:**  
  
-   [Formatos de dados para importar ou exportar em massa](#ComponentsAndConcepts)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Formatos de dados para importar ou exportar em massa  
 A tabela a seguir indica o formato de dados que costuma ser adequado ao uso, dependendo de como os dados estão representados e da origem ou destino da operação.  
  
|Operação|Nativo|Unicode nativo|Caractere|Caractere unicode|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Transferências de dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum caractere estendido ou DBCS (conjunto de caracteres de dois bytes). A menos que um arquivo de formato seja usado, essas tabelas devem ser definidas identicamente.|Sim*|—|—|—|  
|Para colunas **sql_variant** , recomenda-se usar o formato de dados nativos que, ao contrário dos formatos Unicode e de caractere, preservam os metadados de cada valor **sql_variant** .|Sim|—|—|—|  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
