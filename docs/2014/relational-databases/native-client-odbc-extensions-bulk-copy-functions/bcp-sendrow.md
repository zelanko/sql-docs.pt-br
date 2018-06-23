---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 97229063d5ce78ebae1293eb85b05ee8765fc4c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007930"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  Envia uma linha de dados de variáveis de programa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 O **bcp_sendrow** função cria uma linha de variáveis de programa e o envia para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de chamar **bcp_sendrow**, você deve fazer chamadas para [bcp_bind](bcp-bind.md) para especificar as variáveis de programa que contêm dados de linha.  
  
 Caso **bcp_bind** seja chamado especificando um tipo de dados longo de comprimento variável, por exemplo um parâmetro *eDataType* de SQLTEXT e um parâmetro *pData* diferente de NULL, **bcp_sendrow** envia todo o valor de dados, exatamente como faz para qualquer outro tipo de dados. Se, no entanto, **bcp_bind** tem um valor nulo *pData* parâmetro **bcp_sendrow** retorna o controle para o aplicativo imediatamente após todas as colunas com os dados especificados são enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O aplicativo pode chamar [bcp_moretext](bcp-moretext.md) repetidamente para enviar os dados longos e comprimento variável para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma parte de cada vez. Para obter mais informações, consulte [bcp_moretext](bcp-moretext.md).  
  
 Quando **bcp_sendrow** é usado para variáveis de programa para de linhas de cópia em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas, as linhas serão confirmadas apenas quando o usuário chama [bcp_batch](bcp-batch.md) ou [bcp_done](bcp-done.md) . O usuário pode escolher chamar **bcp_batch** uma vez a cada *n* linhas ou quando houver uma pausa entre períodos de dados de entrada. Se **bcp_batch** nunca for chamado, as linhas serão confirmadas quando **bcp_done** for chamado.  
  
 Para obter informações sobre uma quebra de alteração na cópia em massa a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], consulte [executando operações de cópia em massa &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  