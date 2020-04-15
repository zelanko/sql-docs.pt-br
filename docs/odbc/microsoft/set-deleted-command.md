---
title: SET COMANDO EXCLUÍDO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b3302dc7eecca7135dab9dff5afa376169be0f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300876"
---
# <a name="set-deleted-command"></a>Comando SET DELETED
Especifica se os registros marcados para exclusão são processados e se estão disponíveis para uso em outros comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (Padrão para o driver; o padrão para Visual FoxPro é OFF.) Especifica que os comandos que operam em registros (incluindo registros em tabelas relacionadas) usando um escopo ignoram registros marcados para exclusão.  
  
 OFF  
 Especifica que os registros marcados para exclusão podem ser acessados por comandos que operam em registros (incluindo registros em tabelas relacionadas) usando um escopo.  
  
## <a name="remarks"></a>Comentários  
 As consultas que usam EXCLUÍDAS para testar o status dos registros podem ser otimizadas usando a tecnologia Visual FoxPro Rushmore se a tabela for indexada em DELETED( ).  
  
> [!IMPORTANT]  
>  SET DELETED é ignorado se o escopo padrão do comando for o registro atual ou se você incluir um escopo de um único registro. O ÍNDICE sempre ignora SET EXCLUÍDO e indexa todos os registros na tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)
