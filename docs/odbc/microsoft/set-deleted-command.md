---
title: Comando SET DELETED | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997739"
---
# <a name="set-deleted-command"></a>Comando SET DELETED
Especifica se os registros marcados para exclusão são processados e se eles estão disponíveis para uso em outros comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Padrão para o driver; o padrão para o Visual FoxPro é OFF). Especifica que comandos que operam em registros (inclusive os registros em tabelas relacionadas) usando um escopo de ignorar registros marcados para exclusão.  
  
 OFF  
 Especifica que registros marcados para exclusão pode ser acessada pelos comandos que operam em registros (inclusive os registros em tabelas relacionadas) usando um escopo.  
  
## <a name="remarks"></a>Comentários  
 Consulta que uso excluído () para testar o status dos registros pode ser otimizado usando tecnologia Rushmore do Visual FoxPro, se a tabela é indexada em (excluído).  
  
> [!IMPORTANT]  
>  Definir excluído é ignorado se o escopo padrão para o comando é o registro atual ou se você incluir um escopo de um único registro. O índice sempre ignora definido excluídas e indexa todos os registros na tabela.  
  
## <a name="see-also"></a>Consulte também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)
