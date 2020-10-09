---
description: Extensões de driver do SQL Server – Funções de cópia em massa
title: Funções de cópia em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8de90d38e540b4c4964581ef434514bc734cbdf0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866947"
---
# <a name="sql-server-driver-extensions---bulk-copy-functions"></a>Extensões de driver do SQL Server – Funções de cópia em massa
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC (Open Database Connectivity) é uma interface de programação de aplicativo do Microsoft Win32 usada pelos aplicativos para acessar dados em fontes de dados ODBC. A referência do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não documenta todas as chamadas de função do ODBC. Só essas funções com parâmetros ou comportamentos específicos de driver quando usados com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client são abordados.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está em conformidade com a especificação do ODBC 3.51. Para uma referência abrangente do ODBC 3,51, baixe o SDK do Microsoft Data Access Components do [centro de desenvolvedores de acesso a dados e armazenamento](https://go.microsoft.com/fwlink?linkid=4173)ou exiba a referência online [do programador do ODBC](../../odbc/reference/odbc-programmer-s-reference.md) .  
 
 A extensão API de cópia em massa específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que aplicativos cliente adicionem ou extraiam linhas de dados rapidamente de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Ao usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, você pode referenciar as BCP (funções de cópia em massa) em SQLNCLI11.LIB e em SQLNCLI.H.  
  
 Um aplicativo que usa chamadas de função de API BCP deve ser vinculado com a biblioteca (.lib) que é enviada com o driver (.dll) usado pelo aplicativo. Um aplicativo BCP não deve vincular com mais de uma biblioteca de driver.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)  
  
-   [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)  
  
-   [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)  
  
-   [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)  
  
-   [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)  
  
-   [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)  
  
-   [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)  
  
-   [bcp_getcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_gettypename](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-gettypename.md)  
  
-   [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)  
  
-   [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)  
  
-   [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)  
  
-   [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
-   [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de driver de SQL Server]()   
 [Executando operações de cópia em massa &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
