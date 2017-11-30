---
title: Criar aplicativos clientes para dados FILESTREAM | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d0b98d5c89164b220ff4cec69a3a3a2f33af5688
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-client-applications-for-filestream-data"></a>Criar aplicativos clientes para dados FILESTREAM
  Você pode usar as APIs do Win32 para ler e gravar dados em um FILESTREAM BLOB. As seguintes etapas são exigidas:  
  
-   Leia o caminho do arquivo de FILESTREAM.  
  
-   Leia o contexto de transação atual.  
  
-   Obtenha um identificador de Win32 e use-o para ler e gravar dados no FILESTREAM BLOB.  
  
> [!NOTE]  
>  Os exemplos citados neste tópico exigem o banco de dados e a tabela habilitados para FILESTREAM criados em [Criar um banco de dados habilitado para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md) e [Criar uma tabela para armazenar dados de FILESTREAM](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md).  
  
##  <a name="func"></a> Funções para trabalhar com dados FILESTREAM  
 Quando FILESTREAM é usado para armazenar dados BLOB (objeto binário grande), é possível usar APIs do Win32 para trabalhar com os arquivos. Para oferecer suporte ao trabalho com dados BLOB do FILESTREAM em aplicativos Win32, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as seguintes funções e API:  
  
-   [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) retorna um caminho como um token para um BLOB. Um aplicativo usa esse token para obter um identificador do Win32 e operar em dados BLOB.  
  
     Quando o banco de dados que contém dados FILESTREAM pertence a um grupo de disponibilidade AlwaysOn, a função PathName retorna um VNN (nome de rede virtual) em vez de um nome do computador.  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) retorna um token que representa a transação atual de uma sessão. Um aplicativo usa esse token para associar operações de fluxo contínuo do sistema de arquivos do FILESTREAM à transação.  
  
-   A [API OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) obtém um identificador de arquivo Win32. O aplicativo usa o identificador para transmitir os dados do FILESTREAM e, em seguida, pode passar o identificador para as seguintes APIs do Win32: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426), ou [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Se o aplicativo chamar qualquer outra API usando o identificador, um erro ERROR_ACCESS_DENIED será retornado. O aplicativo deve fechar o identificador usando [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428).  
  
 O acesso ao contêiner de dados All FILESTREAM é executado em uma transação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser executadas na mesma transação para manter a consistência entre dados SQL e dados FILESTREAM.  
  
##  <a name="steps"></a> Etapas para acessar dados FILESTREAM  
  
###  <a name="path"></a> Lendo o caminho do arquivo de FILESTREAM  
 Cada célula em uma tabela de FILESTREAM tem um caminho de arquivo associado. Para ler o caminho, use a propriedade **PathName** de uma coluna **varbinary(max)** em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Os exemplos a seguir mostram como ler o caminho de arquivo de uma coluna **varbinary(max)** .  
  
 [!code-sql[FILESTREAM#FS_PathName](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_1.sql)]  
  
###  <a name="trx"></a> Lendo o contexto da transação  
 Para obter o contexto da transação atual, use a função [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) . O exemplo seguinte mostra como começar uma transação e ler o contexto de transação atual.  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_2.sql)]  
  
###  <a name="handle"></a> Obtendo um identificador de arquivo Win32  
 Para obter um identificador de arquivo do Win32, chame a API OpenSqlFilestream. Esta API é exportada do arquivo sqlncli.dll. O identificador retornado pode ser transmitido para qualquer uma das seguintes APIs do Win32: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426), ou [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Os exemplos a seguir mostram como obter um identificador de arquivo Win32 e usá-lo para ler e gravar dados no FILESTREAM BLOB.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/create-client-applicatio_3.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/create-client-applicatio_4.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/create-client-applicatio_5.cpp)]  
  
##  <a name="best"></a> Práticas recomendadas para design e implementação de aplicativos  
  
-   Ao criar e implementar aplicativos que usam FILESTREAM, considere as seguintes diretrizes:  
  
-   Use NULL em vez de 0x representar uma coluna de FILESTREAM não inicializada. O valor 0x faz com que um arquivo seja criado; NULL não faz.  
  
-   Evite operações de inserção e de exclusão em tabelas que contêm colunas de FILESTREAM não nulas. As operações de inserção e de exclusão podem modificar as tabelas de FILESTREAM que são usadas para coleta de lixo. Isso pode fazer com que o desempenho de um aplicativo seja reduzido ao longo do tempo.  
  
-   Em aplicativos que usam replicação, use NEWSEQUENTIALID() em vez de NEWID(). NEWSEQUENTIALID() executa melhor que NEWID() para geração de GUID nesses aplicativos.  
  
-   A API FILESTREAM foi projetada para acesso de streaming do Win32 aos dados. Evite usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para ler ou gravar BLOBs (objetos binários grandes) de FILESTREAM maiores que 2 MB. Se você precisar ler ou gravar dados BLOB de [!INCLUDE[tsql](../../includes/tsql-md.md)], verifique se todos os dados BLOB serão consumidos antes de você tentar abrir o BLOB de FILESTREAM no Win32. O não consumo de todos os dados [!INCLUDE[tsql](../../includes/tsql-md.md)] pode provocar falha em quaisquer operações sucessivas de abertura ou de fechamento de FILESTREAM.  
  
-   Evite instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que atualizam, acrescentam ou precedem dados no BLOB de FILESTREAM. Isso faz com que os dados BLOB sejam colocados no spool no banco de dados tempdb e retornados em um novo arquivo físico.  
  
-   Evite acrescentar atualizações de BLOBs pequenos a um BLOB de FILESTREAM. Cada acréscimo faz com que os arquivos FILESTREAM subjacentes sejam copiados. Se um aplicativo precisar acrescentar BLOBs pequenos, grave os BLOBs em uma coluna **varbinary(max)** e execute uma única operação de gravação no BLOB de FILESTREAM quando o número de BLOBs atingir um limite predeterminado.  
  
-   Evite recuperar o comprimento de dados de muitos arquivos de BLOB em um aplicativo. Essa é uma operação demorada porque o tamanho não é armazenado no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Se você precisar determinar o tamanho de um arquivo de BLOB, use a função DATALENGTH() do [!INCLUDE[tsql](../../includes/tsql-md.md)] para determinar o tamanho do BLOB se ele estiver fechado. A função DATALENGTH() não abre o arquivo de BLOB para determinar seu tamanho.  
  
-   Se um aplicativo usar o protocolo SMB1, os dados BLOB de FILESTREAM deverão ser lidos em múltiplos de 60 KB para otimizar o desempenho.  
  
## <a name="see-also"></a>Consulte também  
 [Evitar conflitos com operações de banco de dados em aplicativos de FILESTREAM](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [Acessar dados do FILESTREAM com OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Fazer atualizações parciais em dados do FILESTREAM](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
  
  
