---
title: Comando SET BLOCKSIZE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e904d341513047b3940cf5b3fc2ba9538cdb5c8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127842"
---
# <a name="set-blocksize-command"></a>Comando SET BLOCKSIZE
Especifica como o espaço em disco é alocado para o armazenamento de campos de memorando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica o tamanho do bloco de alocar espaço em disco para campos de memorando. Se *nBytes* for 0, espaço em disco é alocado em bytes simples (blocos de 1 byte). Se *nBytes* é um número inteiro entre 1 e 32, espaço em disco é alocado em blocos de *nBytes* bytes multiplicado por 512. Se *nBytes* é maior que 32, espaço em disco é alocado em blocos de *nBytes* bytes. Se você especificar um valor de tamanho de bloco maior do que 32, você pode economizar espaço em disco considerável.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão para definir o tamanho de bloco é 64. Para redefinir o tamanho do bloco para um valor diferente depois que o arquivo foi criado, defina-o para um novo valor e, em seguida, usar a cópia para criar uma nova tabela. A nova tabela tem o tamanho de bloco especificado.
