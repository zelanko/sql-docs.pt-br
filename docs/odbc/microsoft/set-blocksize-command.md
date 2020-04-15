---
title: COMANDO BLOCKSIZE SET | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300896"
---
# <a name="set-blocksize-command"></a>Comando SET BLOCKSIZE
Especifica como o espaço em disco é alocado para o armazenamento de campos de memorando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *Nbytes*  
 Especifica o tamanho do bloco no qual o espaço do disco para campos de memorando é alocado. Se *nBytes* for 0, o espaço em disco será alocado em bytes únicos (blocos de 1 byte). Se *nBytes* for um inteiro entre 1 e 32, o espaço em disco será alocado em blocos de *bytes nBytes* multiplicados por 512. Se *nBytes* for maior que 32, o espaço em disco será alocado em blocos de *bytes nBytes.* Se você especificar um valor de tamanho de bloco maior que 32, poderá economizar espaço substancial no disco.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão para SET BLOCKSIZE é 64. Para redefinir o tamanho do bloco para um valor diferente após a criação do arquivo, defina-o como um novo valor e use COPY para criar uma nova tabela. A nova tabela tem o tamanho do bloco especificado.
