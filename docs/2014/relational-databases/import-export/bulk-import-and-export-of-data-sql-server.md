---
title: Importação e exportação em massa de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4bfbd00c0079aec3e9bcfa67560962356be1cad4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227686"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Importação e exportação em massa de dados (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à exportação de dados em massa (*dados em massa*) de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à importação dos dados em massa para uma exibição não particionada ou uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A importação e a exportação em massa são essenciais para transferir os dados de maneira eficiente entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as fontes de dados heterogêneos. *Exportação em massa* se refere à copia de dados de uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados. *Importação em massa* refere-se ao carregamento de dados de um arquivo de dados em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, você pode exportar dados de um aplicativo Excel do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para um arquivo de dados e então importar em massa dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Neste tópico:**  
  
-   [Introdução à importação em massa e operações de exportação em massa](#Intro)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Intro"></a> Importação em massa e visão geral de exportação em massa  
 Esta seção lista e compara brevemente os vários métodos disponíveis para a importação e exportação em massa dos dados. A seção também apresenta arquivos de formato.  
  
 **Neste tópico:**  
  
-   [Métodos para importação e exportação de dados em massa](#MethodsForBuliIE)  
  
-   [Arquivos de formato](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> Métodos para importação e exportação de dados em massa  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à exportação de dados em massa de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à importação de dados em massa em uma tabela ou exibição não particionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os métodos básicos a seguir estão disponíveis.  
  
|Método|Description|Importa dados|Exporta dados|  
|------------|-----------------|------------------|------------------|  
|[utilitário bcp](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Um utilitário de linha de comando (Bcp.exe) que exporta e importa dados em massa e gera arquivos de formato.|Sim|Sim|  
|[instrução BULK INSERT](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que importa dados diretamente de um arquivo de dados para uma tabela de banco de dados ou exibição não particionada.|Sim|não|  
|[Instrução INSERT ... Instrução SELECT * FROM OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que usa o provedor de conjunto de linhas em massa OPENROWSET para importação em massa dos dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificando a função OPENROWSET(BULK...) para selecionar dados em uma instrução INSERT.|Sim|não|  
  
> [!IMPORTANT]  
>  Os arquivos CSV (valores separados por vírgula) não têm suporte nas operações de importação em massa do SQL Server. No entanto, em alguns casos, um arquivo CSV pode ser usado como arquivo de dados para uma importação em massa de dados no SQL Server. Observe que o terminador de campo de um arquivo CSV não tem que ser uma vírgula. Para obter mais informações, consulte [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md).  
  
###  <a name="FFs"></a> Arquivos de formato  
 O utilitário **bcp**, BULK INSERT e INSERT... SELECT \* FROM OPENROWSET(BULK...) dão suporte ao uso de um *arquivo de formato* especializado que armazena informações de formato para cada campo em um arquivo de dados. Um arquivo de formato também pode conter informações sobre a tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente. O arquivo de formato pode ser usado para fornecer todas as informações de formato necessárias para exportar e importar dados em massa para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os arquivos de formato fornecem um modo flexível para interpretar dados como eles são no arquivo de dados durante a importação, e também formatar dados no arquivo de dados durante a exportação. Essa flexibilidade elimina a necessidade de gravar um código com finalidade especial para interpretar os dados ou reformatar os dados segundo requisitos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o aplicativo externo. Por exemplo, se você estiver exportando dados em massa para serem carregados em um aplicativo que exige valores separados por vírgula, use um arquivo de formato para inserir vírgulas como terminadores de campo nos dados exportados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de arquivos de formato: arquivos de formato XML e não XML.  
  
 O utilitário **bcp** é a única ferramenta que pode gerar um arquivo de formato. Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md). Para obter mais informações sobre os arquivos de formato, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
> [!NOTE]  
>  Se um arquivo de formato não for fornecido durante uma operação de exportação ou importação em massa, você poderá substituir a formatação padrão na linha de comando.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Importar e exportar em massa dados usando o utilitário bcp &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK... &#41; &#40;Do SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar um arquivo de formato**  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de dados para compatibilidade usando bcp**  
  
1.  [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos para log mínimo em importação em massa](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [Copiar bancos de dados em outros servidores](../databases/copy-databases-to-other-servers.md)   
 [Executando o carregamento em massa de dados XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [Executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
