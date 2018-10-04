---
title: Método STAT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 127aab5e00247ce5550f25e2a281e190472b0186
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828224"
---
# <a name="stat-method"></a>Método Stat
Recupera informações sobre um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **longo** valor que indica o status da operação.  
  
#### <a name="parameters"></a>Parâmetros  
 *StatStg*  
 Uma estrutura STATSTG que será preenchida com informações sobre o fluxo. A implementação do **Stat** método usado pelo objeto ADO Stream não preenche todos os campos da estrutura.  
  
 *StatFlag*  
 Especifica que esse método não retorna alguns dos membros na estrutura de STATSTG, economizando uma operação de alocação de memória. Os valores são tirados da enumeração STATFLAG. A enumeração STATFLAG tem dois valores  
  
|Constante|Valor|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Comentários  
 A versão do método Stat implementado para o objeto Stream ADO preenche os campos seguintes da estrutura STATSTG:  
  
 *pwcsName*  
 Uma cadeia de caracteres que contém o nome do fluxo, se houver uma disponível e o valor de StatFlag STATFLAG_NONAME não foi especificada.  
  
 *cbSize*  
 Especifica o tamanho em bytes da matriz de bytes ou fluxo.  
  
 *mtime*  
 Indica a hora da última modificação para este armazenamento, fluxo ou matriz de bytes.  
  
 *ctime*  
 Indica a hora de criação para este armazenamento, fluxo ou matriz de bytes.  
  
 *atime*  
 Indica a hora do último acesso para este armazenamento, fluxo ou matriz de bytes.  
  
 Se STATFLAG_NONAME for especificado no parâmetro StatFlag, o nome do fluxo não é retornado.  
  
 Se STATFLAG_NONAME não foi especificado no parâmetro StatFlag e nenhum nome está disponível para o fluxo atual, esse valor será E_NOTIMPL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
