---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_columns
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d26f288c857cf44a932a91b250074c36453e2482
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73782980"
---
# <a name="bcp_columns"></a>bcp_columns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Define o número total de colunas encontrado no arquivo de usuário para uso com uma cópia em massa dentro ou fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) pode ser usado em vez de bcp_columns e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_columns (  
        HDBC hdbc,  
        INT nColumns);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *nColumns*  
 É o número total de colunas no arquivo de usuário. Mesmo que você esteja se preparando para copiar dados em massa do arquivo de usuário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma tabela e não pretende copiar todas as colunas no arquivo de usuário, você ainda deve definir *nColumns* para o número total de colunas do arquivo de usuário.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Essa função pode ser chamada somente depois que [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) tiver sido chamado com um nome de arquivo válido.  
  
 Você só deveria chamar esta função se pretender usar um formato de arquivo de usuário diferente do padrão. Para obter mais informações sobre uma descrição do formato de arquivo de usuário padrão, consulte **bcp_init**.  
  
 Depois de chamar **bcp_columns**, você deve chamar [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) para cada coluna no arquivo de usuário para definir completamente um formato de arquivo personalizado.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
