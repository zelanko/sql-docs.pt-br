---
title: CONJUNTO BLOCKSIZE comando | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3bcb1e8da857fb4c0b45fce99da189e228e0a53d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="set-blocksize-command"></a>Comando do conjunto de tamanho de bloco
Especifica como o espaço em disco é alocado para o armazenamento de campos de memorando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica o tamanho do bloco no qual o espaço em disco para campos de memorando é alocado. Se *nBytes* for 0, espaço em disco alocado em bytes simples (blocos de 1 byte). Se *nBytes* é um inteiro entre 1 e 32, espaço em disco é alocado em blocos de *nBytes* bytes multiplicado por 512. Se *nBytes* é maior do que 32, o espaço em disco alocado em blocos de *nBytes* bytes. Se você especificar um valor de tamanho de bloco maior do que 32, você pode economizar espaço em disco considerável.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão para definir o tamanho de bloco é 64. Para redefinir o tamanho do bloco para um valor diferente depois que o arquivo foi criado, defina-o para um novo valor e, em seguida, usar a cópia para criar uma nova tabela. A nova tabela tem o tamanho de bloco especificado.
