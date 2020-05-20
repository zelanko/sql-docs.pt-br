---
title: Método stat | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: rothja
ms.author: jroth
ms.openlocfilehash: 6295640a0d9ec0815ebac9086efc3835915e0e0c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759772"
---
# <a name="stat-method"></a>Método Stat
Recupera informações sobre um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **longo** que indica o status da operação.  
  
#### <a name="parameters"></a>Parâmetros  
 *StatStg*  
 Uma estrutura STATSTG que será preenchida com informações sobre o fluxo. A implementação do método **stat** usado pelo objeto de fluxo ADO não preenche todos os campos da estrutura.  
  
 *StatFlag*  
 Especifica que esse método não retorna alguns dos membros na estrutura STATSTG, salvando assim uma operação de alocação de memória. Os valores são obtidos da enumeração STATFLAG. A enumeração STATFLAG tem dois valores  
  
|Constante|Valor|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Comentários  
 A versão do método stat implementada para o objeto de fluxo ADO preenche os seguintes campos da estrutura STATSTG:  
  
 *pwcsName*  
 Uma cadeia de caracteres que contém o nome do fluxo, se houver um disponível e o valor de StatFlag STATFLAG_NONAME não foi especificado.  
  
 *cbSize*  
 Especifica o tamanho em bytes da matriz de bytes ou fluxo.  
  
 *mtime*  
 Indica a hora da última modificação desse armazenamento, fluxo ou matriz de bytes.  
  
 *ctime*  
 Indica a hora de criação desse armazenamento, fluxo ou matriz de bytes.  
  
 *atime*  
 Indica a hora do último acesso desse armazenamento, fluxo ou matriz de bytes.  
  
 Se STATFLAG_NONAME for especificado no parâmetro StatFlag, o nome do fluxo não será retornado.  
  
 Se STATFLAG_NONAME não tiver sido especificado no parâmetro StatFlag e não houver nenhum nome disponível para o fluxo atual, esse valor será E_NOTIMPL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
