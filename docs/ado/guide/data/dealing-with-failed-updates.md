---
title: "Lidando com atualizações com falha | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dc8facd3f93f0c752739c20d61352d8c4ab2f63f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="dealing-with-failed-updates"></a>Lidando com atualizações com falha
Quando uma atualização é concluída com erros, como resolver os erros depende a natureza e a severidade dos erros e a lógica do seu aplicativo. No entanto, se o banco de dados for compartilhado com outros usuários, um erro comum é que outra pessoa modificar o campo antes de fazer. Esse tipo de erro é chamado de um conflito. ADO detectará essa situação e relata um erro.  
  
## <a name="remarks"></a>Comentários  
 Se houver erros de atualização, eles serão capturados em uma rotina de tratamento de erros. Filtre o conjunto de registros com a constante adFilterConflictingRecords para que somente as linhas conflitantes são visíveis. Neste exemplo, a estratégia de resolução de erro é apenas imprimir o autor nomes e sobrenomes (au_fname e au_lname).  
  
 O código para alertar o usuário para o conflito de atualização tem esta aparência:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)

