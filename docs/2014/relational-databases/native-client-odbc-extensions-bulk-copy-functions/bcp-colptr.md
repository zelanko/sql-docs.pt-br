---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: rothja
ms.author: jroth
ms.openlocfilehash: 90170f586fb51794697308b09e46dbe5ff3a65f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019647"
---
# <a name="bcp_colptr"></a>bcp_colptr
  Define o endereço de dados variáveis do programa da cópia atual no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *pData*  
 É um ponteiro para os dados a serem copiados. Se o tipo de dados associado for um tipo de valor grande (como SQLTEXT ou SQLIMAGE), *pData* poderá ser NULL. Um *pData* nulo indica que valores de dados longos serão enviados para SQL Server em partes usando [bcp_moretext](bcp-moretext.md).  
  
 Se *pData* for definido como NULL e a coluna correspondente ao campo associado não for um tipo de valor grande, **bcp_colptr** falhará.  
  
 Para obter mais informações sobre tipos de valor grande, consulte [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 É a posição ordinal da coluna na tabela do banco de dados na qual os dados são copiados. A primeira coluna em uma tabela é a coluna 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 A função **bcp_colptr** permite que você altere o endereço dos dados de origem de uma determinada coluna ao copiar dados para SQL Server com [bcp_sendrow](bcp-sendrow.md).  
  
 Inicialmente, o ponteiro para os dados do usuário é definido por uma chamada para **bcp_bind**. Se o endereço de dados da variável do programa for alterado entre as chamadas para **bcp_sendrow**, você poderá chamar **bcp_colptr** para redefinir o ponteiro para os dados. A próxima chamada para **bcp_sendrow** envia os dados endereçados pela chamada para **bcp_colptr**.  
  
 Deve haver uma chamada **bcp_colptr** separada para cada coluna na tabela cujo endereço de dados você deseja modificar.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
