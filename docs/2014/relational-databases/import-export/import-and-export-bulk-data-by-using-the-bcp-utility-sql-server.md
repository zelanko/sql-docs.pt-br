---
title: Importar e exportar dados em massa usando o utilitário bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c16ceceac2f4ddfed82605e18cac30f15894d702
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130559"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importar e exportar dados em massa usando o utilitário bcp (SQL Server)
  Este tópico oferece uma visão geral de como usar o [utilitário bcp](../../tools/bcp-utility.md) para exportar dados de qualquer lugar para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em que uma instrução SELECT atua, incluindo exibições particionadas.  
  
 O utilitário bcp (Bcp.exe) é uma ferramenta de linha de comandos que usa a API do BCP (Programa de cópia em massa). O utilitário bcp executa as seguintes tarefas:  
  
-   Exporta dados em massa de uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados.  
  
-   Exporta dados em massa de uma consulta.  
  
-   Importa dados em massa de um arquivo de dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Gera arquivos de formato.  
  
 O utilitário bcp é acessado pelo comando **bcp** . Caso não esteja usando um arquivo de formato preexistente, para usar o comando **bcp** para importar dados em massa, será necessário compreender o esquema da tabela e os tipos de dados de suas colunas.  
  
 O utilitário bcp pode exportar dados de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados para uso em outros programas. O utilitário também pode importar dados de outro programa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , geralmente outro DBMS (sistema de gerenciamento de banco de dados). Os dados são exportados primeiro do programa de origem para um arquivo de dados e, depois, em uma operação separada, copiados do arquivo de dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O comando **bcp** oferece opções que você usa para especificar o tipo de dados do arquivo de dados e outras informações. Se essas opções não forem especificadas, o comando sugere formatar as informações, como o tipo de campos de dados em um arquivo de dados. O comando pergunta se você quer criar um arquivo de formato que contém suas respostas interativas. Se você quiser flexibilidade para operações futuras de importação ou exportação em massa, um arquivo de formato é sempre útil. Você pode especificar o arquivo de formato em comandos **bcp** posteriores para arquivos de dados equivalentes. Para obter mais informações, veja [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  O utilitário bcp é gravado usando a cópia em massa do ODBC  
  
 Para obter uma descrição da sintaxe do comando **bcp**, veja [Utilitário bcp](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos do **bcp**, veja:  
  
-   [Utilitário bcp](../../tools/bcp-utility.md)  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [Cláusula SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Preparar para importar dados em massa &#40;SQL Server&#41;](prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
  
