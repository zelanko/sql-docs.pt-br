---
title: Definir comando BLOCKSIZE | Microsoft Docs
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
ms.openlocfilehash: 4fe84a470f5e877c73701168394cd85d75253fb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997754"
---
# <a name="set-blocksize-command"></a>Comando SET BLOCKSIZE
Especifica como o espaço em disco é alocado para o armazenamento de campos de memorando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica o tamanho do bloco no qual o espaço em disco para campos de memorando é alocado. Se *nbytes* for 0, o espaço em disco será alocado em bytes únicos (blocos de 1 byte). Se *nbytes* for um inteiro entre 1 e 32, o espaço em disco será alocado em blocos de *nbytes* bytes multiplicados por 512. Se *nbytes* for maior que 32, o espaço em disco será alocado em blocos de *nbytes* bytes. Se você especificar um valor de tamanho de bloco maior que 32, poderá economizar espaço em disco significativo.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão para SET BLOCKSIZE é 64. Para redefinir o tamanho do bloco para um valor diferente depois que o arquivo tiver sido criado, defina-o como um novo valor e, em seguida, use Copiar para criar uma nova tabela. A nova tabela tem o tamanho de bloco especificado.
