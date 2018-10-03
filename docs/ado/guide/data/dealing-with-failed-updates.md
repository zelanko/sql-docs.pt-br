---
title: Lidando com falha nas atualizações | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6ba4b4189691bf907b3ad67db91a8534268a8ec0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616424"
---
# <a name="dealing-with-failed-updates"></a>Lidar com atualizações de falha
Quando uma atualização é concluído com erros, como você resolver os erros depende da natureza e gravidade dos erros e a lógica do seu aplicativo. No entanto, se o banco de dados for compartilhado com outros usuários, um erro comum é que alguém modifica o campo antes de fazer. Esse tipo de erro é chamado um conflito. ADO detectará essa situação e relata um erro.  
  
## <a name="remarks"></a>Comentários  
 Se houver erros de atualização, eles serão capturados em uma rotina de tratamento de erros. Filtre o conjunto de registros com a constante adFilterConflictingRecords, de modo que somente as linhas conflitantes são visíveis. Neste exemplo, a estratégia de resolução de erro é meramente imprimir o autor nomes e sobrenomes (au_fname e au_lname).  
  
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
