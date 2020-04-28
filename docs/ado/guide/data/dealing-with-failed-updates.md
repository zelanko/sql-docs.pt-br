---
title: Lidando com atualizações com falha | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d442a9c397ad184658f9101343e139697c9b3756
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925631"
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
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
