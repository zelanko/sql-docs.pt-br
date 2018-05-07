---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: baf75dd4d0c9c040573a54dd102f38ef3ecd4f21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bcpsendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Envia uma linha de dados de variáveis de programa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 O **bcp_sendrow** função cria uma linha de variáveis de programa e o envia para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de chamar **bcp_sendrow**, você deve fazer chamadas para [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para especificar as variáveis de programa que contêm dados de linha.  
  
 Se **bcp_bind** seja chamado especificando um tipo de dados longos de comprimento variável, por exemplo, um *eDataType* parâmetro de SQLTEXT e não NULL *pData* parâmetro, **bcp_sendrow** envia o valor de inteiro de dados, assim como faz para qualquer outro tipo de dados. Se, no entanto, **bcp_bind** tem um valor nulo *pData* parâmetro **bcp_sendrow** retorna o controle para o aplicativo imediatamente após todas as colunas com os dados especificados são enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O aplicativo pode chamar [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) repetidamente para enviar os dados longos e comprimento variável para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma parte de cada vez. Para obter mais informações, consulte [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Quando **bcp_sendrow** é usado para variáveis de programa para de linhas de cópia em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas, as linhas serão confirmadas apenas quando o usuário chama [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) ou [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . O usuário pode escolher chamar **bcp_batch** uma vez a cada *n* linhas ou quando houver uma pausa entre períodos de dados de entrada. Se **bcp_batch** nunca for chamado, as linhas serão confirmadas quando **bcp_done** for chamado.  
  
 Para obter informações sobre uma quebra de alteração na cópia em massa a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], consulte [executando operações de cópia em massa &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
