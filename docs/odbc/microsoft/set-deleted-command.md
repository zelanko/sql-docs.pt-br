---
title: "CONJUNTO excluído comando | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3bf1ec522bee6fda19349a71c894ebd98bd75b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="set-deleted-command"></a>Comando do conjunto excluído
Especifica se os registros marcados para exclusão são processados e se eles estão disponíveis para uso em outros comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Padrão para o driver; o padrão para o Visual FoxPro é OFF). Especifica que comandos que operam em registros (inclusive os registros em tabelas relacionadas) usando um escopo de ignorar os registros marcados para exclusão.  
  
 OFF  
 Especifica que registros marcados para exclusão pode ser acessada por comandos que operam em registros (inclusive os registros em tabelas relacionadas) usando um escopo.  
  
## <a name="remarks"></a>Comentários  
 Consulta que use excluído () para testar o status dos registros pode ser otimizado usando a tecnologia Rushmore do Visual FoxPro se a tabela estiver indexada em (excluídos).  
  
> [!IMPORTANT]  
>  Definir excluída será ignorada se o escopo padrão para o comando é o registro atual ou se você incluir um escopo de um único registro. O índice sempre ignora definido excluídas e todos os registros na tabela de índices.  
  
## <a name="see-also"></a>Consulte também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)

