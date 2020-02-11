---
title: Funções de cópia em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2888f34c1e4c4103845d07e569a0dbabeb2e4caa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63225538"
---
# <a name="bulk-copy-functions"></a>Bulk Copy Functions
  A extensão API de cópia em massa específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que aplicativos cliente adicionem ou extraiam linhas de dados rapidamente de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ao usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, você pode referenciar as BCP (funções de cópia em massa) em SQLNCLI11.LIB e em SQLNCLI.H.  
  
 Um aplicativo que usa chamadas de função de API BCP deve ser vinculado com a biblioteca (.lib) que é enviada com o driver (.dll) usado pelo aplicativo. Um aplicativo BCP não deve vincular com mais de uma biblioteca de driver.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [bcp_batch](bcp-batch.md)  
  
-   [bcp_bind](bcp-bind.md)  
  
-   [bcp_colfmt](bcp-colfmt.md)  
  
-   [bcp_collen](bcp-collen.md)  
  
-   [bcp_colptr](bcp-colptr.md)  
  
-   [bcp_columns](bcp-columns.md)  
  
-   [bcp_control](bcp-control.md)  
  
-   [bcp_done](bcp-done.md)  
  
-   [bcp_exec](bcp-exec.md)  
  
-   [bcp_getcolfmt](bcp-getcolfmt.md)  
  
-   [bcp_gettypename](bcp-gettypename.md)  
  
-   [bcp_init](bcp-init.md)  
  
-   [bcp_moretext](bcp-moretext.md)  
  
-   [bcp_readfmt](bcp-readfmt.md)  
  
-   [bcp_sendrow](bcp-sendrow.md)  
  
-   [bcp_setbulkmode](bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](bcp-setcolfmt.md)  
  
-   [bcp_writefmt](bcp-writefmt.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de driver de SQL Server](../../database-engine/dev-guide/sql-server-driver-extensions.md)   
 [Executando operações de cópia em massa &#40;&#41;ODBC](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
