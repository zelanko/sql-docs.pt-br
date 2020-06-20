---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: rothja
ms.author: jroth
ms.openlocfilehash: d634f393b18124e6ae0db753def2c31860f91a74
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019639"
---
# <a name="bcp_columns"></a>bcp_columns
  Define o número total de colunas encontrado no arquivo de usuário para uso com uma cópia em massa dentro ou fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [bcp_setbulkmode](bcp-setbulkmode.md) pode ser usado em vez de bcp_columns e [bcp_colfmt](bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *nColumns*  
 É o número total de colunas no arquivo de usuário. Mesmo que você esteja se preparando para copiar dados em massa do arquivo de usuário para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela e não pretende copiar todas as colunas no arquivo de usuário, você ainda deve definir *nColumns* para o número total de colunas do arquivo de usuário.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Essa função pode ser chamada somente depois que [bcp_init](bcp-init.md) tiver sido chamado com um nome de arquivo válido.  
  
 Você só deveria chamar esta função se pretender usar um formato de arquivo de usuário diferente do padrão. Para obter mais informações sobre uma descrição do formato de arquivo de usuário padrão, consulte **bcp_init**.  
  
 Depois de chamar `bcp_columns` , você deve chamar [bcp_colfmt](bcp-colfmt.md)para cada coluna no arquivo de usuário para definir completamente um formato de arquivo personalizado.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
