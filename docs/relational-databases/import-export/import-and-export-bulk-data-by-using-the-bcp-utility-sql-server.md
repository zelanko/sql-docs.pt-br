---
title: Importar e exportar dados em massa usando o utilitário bcp (SQL Server) | Microsoft Docs
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/28/2016
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0a1a510e717ebb962f39c3b0bb1a342ef52751d
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708004"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importar e exportar dados em massa usando o utilitário bcp (SQL Server)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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

- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)

- [Cláusula SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)

- [Utilitário bcp](../../tools/bcp-utility.md)

- [Preparar a importação de dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)

- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)

- [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)

- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)

- [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)