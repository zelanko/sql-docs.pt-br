---
title: Importar dados em massa usando BULK INSERT ou OPENROWSET(BULK...)(SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7fc748d4db517846a890850cba1198e940f9a395
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="import-bulk-data-by-using-bulk-insert-or-openrowsetbulk-sql-server"></a>Importar Dados em Massa Usando BULK INSERT ou OPENROWSET(BULK...) (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este tópico fornece uma visão geral de como usar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT e a instrução INSERT...SELECT * FROM OPENROWSET(BULK...) para importação em massa de dados de um arquivo de dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este tópico também descreve considerações de segurança sobre o uso de BULK INSERT e OPENROWSET(BULK...) e o uso desses métodos para importação em massa de uma fonte de dados remotos.  
  
> [!NOTE]
> Para usar BULK INSERT ou OPENROWSET(BULK...), é importante entender como a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controla a representação. Para obter mais informações, consulte "Considerações sobre segurança", posteriormente neste tópico.  
  
## <a name="bulk-insert-statement"></a>instrução BULK INSERT  
 BULK INSERT carrega dados de um arquivo de dados em uma tabela. Essa funcionalidade é semelhante àquela fornecida pela opção **in** do comando **bcp** ; no entanto, o arquivo de dados é lido pelo processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter uma descrição da sintaxe de BULK INSERT, consulte [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="bulk-insert-examples"></a>Exemplos de BULK INSERT  
 
  
-   [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="openrowsetbulk-function"></a>Função OPENROWSET(BULK...)  
 O provedor de conjuntos de linhas em massa OPENROWSET é acessado chamando a função OPENROWSET e especificando a opção BULK. A função OPENROWSET(BULK...) permite acessar dados remotos conectando-se a uma fonte de dados remota, como um arquivo de dados, por meio de um provedor OLE DB.  

**Aplica-se a:** `OPENROWSET` não está disponível em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].
  
 Para importar dados em massa, chame OPENROWSET (BULK...) de uma cláusula SELECT...FROM dentro de uma instrução INSERT. A sintaxe básica para importar dados em massa é:  
  
 INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 Quando usada em uma instrução INSERT, OPENROWSET(BULK...) dá suporte a dicas de tabela. Além das dicas de tabela comuns, como TABLOCK, a cláusula BULK pode aceitar as seguinte dicas de tabela especializadas: IGNORE_CONSTRAINTS (ignora somente as restrições CHECK), IGNORE_TRIGGERS, KEEPDEFAULTS e KEEPIDENTITY. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para obter informações sobre usos adicionais da opção de BULK, consulte [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>Instruções INSERT...SELECT * FROM OPENROWSET(BULK...) – exemplos:
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="security-considerations"></a>Considerações sobre segurança  
 Se um usuário usar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o perfil de segurança da conta de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado. Um logon que usa a autenticação do SQL Server não pode ser autenticado fora do Mecanismo de Banco de Dados. Assim, quando um comando BULK INSERT é iniciado por um logon que usa a autenticação do SQL Server, a conexão aos dados é feita por meio do contexto de segurança da conta de processo do SQL Server (a conta usada pelo serviço de Mecanismo de Banco de Dados do SQL Server). 
 
 Para ler a fonte de dados com êxito, você deve dar à conta usada pelo Mecanismo de Banco de Dados do SQL Server acesso ao banco de dados. Em contrapartida, se um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetuar logon por meio da Autenticação do Windows, o usuário pode acessar, no modo somente leitura, aqueles arquivos que podem ser acessados pela conta do usuário, a despeito do perfil de segurança do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Por exemplo, considere um usuário que efetuou logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a Autenticação do Windows. Para que o usuário seja capaz de usar BULK INSERT ou OPENROWSET para importar dados de um arquivo de dados em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conta do usuário requer acesso de leitura ao arquivo de dados. Com acesso ao arquivo de dados, o usuário poderá importar dados do arquivo em uma tabela mesmo se o processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver permissão para acessar o arquivo. O usuário não tem que conceder permissão do acesso de arquivo ao processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] do Windows podem ser configurados para permitir que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja conectada a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remetendo as credenciais de um usuário autenticado do Windows. Esse arranjo é conhecido como *representação* ou *delegação*. Entender como a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlam a segurança por representação de usuário é importante para usar BULK INSERT ou OPENROWSET. Representação de usuário permite que o arquivo de dados resida em um computador diferente que o processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o usuário. Por exemplo, se um usuário no **Computador_A** tiver acesso a um arquivo de dados no **Computador_B**, e a delegação de credenciais tiver sido definida adequadamente, o usuário poderá se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada no **Computador_C**, acessar o arquivo de dados no **Computador_B**e importar dados em massa desse arquivo em uma tabela no **Computador_C**.  
  
## <a name="bulk-importing-from-a-remote-data-file"></a>Importação em massa de um arquivo de dados remoto  
 Para usar BULK INSERT ou INSERT...SELECT \* FROM OPENROWSET(BULK...) para importação de dados em massa de outro computador, o arquivo de dados deve ser compartilhado entre os dois computadores. Para especificar um arquivo de dados compartilhado, use sua UNC que utiliza o formato geral **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*. Além disso, a conta usada para acessar o arquivo de dados deve ter as permissões necessárias para leitura do arquivo no disco remoto.  
  
 Por exemplo, a instrução `BULK INSERT` a seguir importa dados em massa na tabela `SalesOrderDetail` do banco de dados `AdventureWorks` de um arquivo de dados denominado `newdata.txt`. Esse arquivo de dados reside em uma pasta compartilhada denominada `\dailyorders` em um diretório compartilhado de rede denominado `salesforce` em um sistema denominado `computer2`.  
  
```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> [!NOTE]
> Essa restrição não se aplica ao utilitário **bcp** porque o cliente lê o arquivo independentemente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Cláusula SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
