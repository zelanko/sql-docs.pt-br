---
title: Funções de cópia em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b37894b20d7b1eaa04901cf27e716b29f4975fbd
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35702467"
---
# <a name="sql-server-driver-extensions---bulk-copy-functions"></a>Extensões de Driver do SQL Server - funções de cópia em massa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC (Open Database Connectivity) é uma interface de programação de aplicativo do Microsoft Win32 usada pelos aplicativos para acessar dados em fontes de dados ODBC. A referência do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não documenta todas as chamadas de função do ODBC. Só essas funções com parâmetros ou comportamentos específicos de driver quando usados com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client são abordados.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está em conformidade com a especificação do ODBC 3.51. Para obter uma referência abrangente do ODBC 3.51, baixe o Microsoft Data Access Components SDK do [Data Access and Storage Developer Center](http://go.microsoft.com/fwlink?linkid=4173), ou exibir o [referência do programador de ODBC](http://go.microsoft.com/fwlink/?LinkId=45250) on-line.  
 
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
  
## <a name="see-also"></a>Consulte também  
 [Extensões de Driver do SQL Server](http://msdn.microsoft.com/library/1043bc93-965d-4939-bd1c-21e9d8d3e9ac)   
 [Executando operações de cópia em massa &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
