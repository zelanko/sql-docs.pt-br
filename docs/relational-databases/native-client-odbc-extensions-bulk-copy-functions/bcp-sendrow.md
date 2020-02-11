---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4bb5375de9769046c12f56f91d5c26e41090564b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73782499"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Envia uma linha de dados de variáveis de programa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 A função **bcp_sendrow** compila uma linha de variáveis de programa e a envia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de chamar **bcp_sendrow**, você deve fazer chamadas para [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para especificar as variáveis de programa que contêm os dados da linha.  
  
 Se **bcp_bind** for chamado especificando um tipo de dados Long de comprimento variável, por exemplo, um parâmetro *EDATATYPE* de SQLTEXT e um parâmetro *pData* não nulo, **bcp_sendrow** enviará o valor de dados inteiro, assim como faz para qualquer outro tipo de dados. Entretanto, se **bcp_bind** tiver um parâmetro *pData* igual a NULL, **bcp_sendrow** retorna o controle para o aplicativo imediatamente após todas as colunas com os dados especificados serem enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Então, o aplicativo pode chamar [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) repetidamente para enviar os dados longos de comprimento variável para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma parte de cada vez. Para obter mais informações, consulte [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Quando **bcp_sendrow** for usado para copiar linhas em massa de variáveis do programa para tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , as linhas são confirmadas somente quando o usuário chamar [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) ou [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). O usuário pode escolher chamar **bcp_batch** uma vez a cada *n* linhas ou quando houver uma pausa entre períodos de dados de entrada. Se **bcp_batch** nunca for chamado, as linhas serão confirmadas quando **bcp_done** for chamado.  
  
 Para obter informações sobre uma alteração significativa na cópia em massa a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partir do, consulte [executando operações de cópia em massa &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
