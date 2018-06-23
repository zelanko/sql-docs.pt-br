---
title: bcp_colptr | Microsoft Docs
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
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c0fa867ec82520f1dcc0def040d7a8edf8a2a713
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118338"
---
# <a name="bcpcolptr"></a>bcp_colptr
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
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *pData*  
 É um ponteiro para os dados a serem copiados. Se o tipo de dados associado é o tipo de valor grande (por exemplo, SQLTEXT ou SQLIMAGE) *pData* pode ser NULL. Um valor nulo *pData* indica valores de dados longos serão enviados para o SQL Server em partes usando [bcp_moretext](bcp-moretext.md).  
  
 Se *pData* é definido como NULL e a coluna correspondente ao campo associado não é um tipo de valor grande, **bcp_colptr** falhar.  
  
 Para obter mais informações sobre tipos de valor grande, consulte [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 É a posição ordinal da coluna na tabela do banco de dados na qual os dados são copiados. A primeira coluna em uma tabela é a coluna 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 O **bcp_colptr** função permite que você altere o endereço dos dados de origem para uma determinada coluna ao copiar dados para o SQL Server com [bcp_sendrow](bcp-sendrow.md).  
  
 Inicialmente, o ponteiro para dados de usuário é definido por uma chamada para **bcp_bind**. Se o endereço de dados da variável de programa for alterado entre chamadas para **bcp_sendrow**, você pode chamar **bcp_colptr** para redefinir o ponteiro para os dados. A próxima chamada para **bcp_sendrow** envia os dados endereçados pela chamada para **bcp_colptr**.  
  
 Deve haver um separado **bcp_colptr** chamada para cada coluna na tabela cujos endereços de dados você deseja modificar.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  