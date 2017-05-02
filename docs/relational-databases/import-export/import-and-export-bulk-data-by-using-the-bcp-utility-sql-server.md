---
title: "Importar e exportar dados em massa usando o utilitário bcp (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 789069f32f8ff5acd7e57ba742768b0ea7e5c3ea
ms.lasthandoff: 04/11/2017

---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importar e exportar dados em massa usando o utilitário bcp (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Este tópico oferece uma visão geral de como usar o [utilitário bcp](../../tools/bcp-utility.md) para exportar dados de qualquer lugar para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em que uma instrução SELECT atua, incluindo exibições particionadas.  
  
 O utilitário bcp (Bcp.exe) é uma ferramenta de linha de comandos que usa a API do BCP (Programa de cópia em massa). O utilitário bcp executa as seguintes tarefas:  
  
-   Exporta dados em massa de uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados.  
  
-   Exporta dados em massa de uma consulta.  
  
-   Importa dados em massa de um arquivo de dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Gera arquivos de formato.  
  
 O utilitário bcp é acessado pelo comando **bcp** . Caso não esteja usando um arquivo de formato preexistente, para usar o comando **bcp** para importar dados em massa, será necessário compreender o esquema da tabela e os tipos de dados de suas colunas.  
  
 O utilitário bcp pode exportar dados de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados para uso em outros programas. O utilitário também pode importar dados de outro programa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , geralmente outro DBMS (sistema de gerenciamento de banco de dados). Os dados são exportados primeiro do programa de origem para um arquivo de dados e, depois, em uma operação separada, copiados do arquivo de dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O comando **bcp** oferece opções que você usa para especificar o tipo de dados do arquivo de dados e outras informações. Se essas opções não forem especificadas, o comando sugere formatar as informações, como o tipo de campos de dados em um arquivo de dados. O comando pergunta se você quer criar um arquivo de formato que contém suas respostas interativas. Se você quiser flexibilidade para operações futuras de importação ou exportação em massa, um arquivo de formato é sempre útil. Você pode especificar o arquivo de formato em comandos **bcp** posteriores para arquivos de dados equivalentes. Para obter mais informações, veja [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
>**Observação:** O utilitário bcp é gravado usando a cópia em massa do ODBC.
  
 Para obter uma descrição da sintaxe do comando **bcp** , veja [Utilitário bcp](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Exemplos  
|Os tópicos a seguir contêm exemplos sobre como usar o bcp: |
|---|
|[bcp Utility](../../tools/bcp-utility.md)<br /><br />Formatos de dados para importar ou exportar em massa (SQL Server)<br />&emsp;&#9679;&emsp;[Usar o formato nativo para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato nativo Unicode para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[Especificar terminadores de campo e linha (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[Manter valores nulos ou use os valores padrão durante a importação em massa (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[Manter valores de identidade ao importar dados em massa (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />Arquivos de formato para importação ou exportação de dados (SQL Server))<br />&emsp;&#9679;&emsp;[Criar um formato de arquivo (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para importação em massa de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar um campo de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[Exemplos de importação e exportação em massa de documentos XML (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

  
## <a name="more-examples-and-information"></a>Mais exemplos e informações  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Cláusula SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [Preparar para importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
  

