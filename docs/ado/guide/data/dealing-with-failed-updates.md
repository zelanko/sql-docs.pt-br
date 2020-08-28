---
description: Lidar com atualizações de falha
title: Lidando com atualizações com falha | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: ca4c5a094e263ca0c44c58a9d9118d4e2ce01538
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991407"
---
# <a name="dealing-with-failed-updates"></a>Lidar com atualizações de falha
Quando uma atualização é concluída com erros, a maneira como você resolve os erros depende da natureza e da severidade dos erros e da lógica do seu aplicativo. No entanto, se o banco de dados for compartilhado com outros usuários, um erro típico é que outra pessoa modifica o campo antes de fazer isso. Esse tipo de erro é chamado de conflito. O ADO detecta essa situação e relata um erro.  
  
## <a name="remarks"></a>Comentários  
 Se houver erros de atualização, eles serão interceptados em uma rotina de tratamento de erros. Filtre o conjunto de registros com a constante adFilterConflictingRecords para que apenas as linhas conflitantes fiquem visíveis. Neste exemplo, a estratégia de resolução de erros é simplesmente imprimir o nome e o sobrenome do autor (au_fname e au_lname).  
  
 O código para alertar o usuário para o conflito de atualização é semelhante ao seguinte:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de lote](./batch-mode.md)