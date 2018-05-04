---
title: CONJUNTO excluído comando | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e05a05b27be43423dd526efccf28e6c2f686f205
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 Consulta que use excluído () para testar o status dos registros pode ser otimizado usando a tecnologia Rushmore do Visual FoxPro se a tabela estiver indexada em (excluídos).  
  
> [!IMPORTANT]  
>  Definir excluída será ignorada se o escopo padrão para o comando é o registro atual ou se você incluir um escopo de um único registro. O índice sempre ignora definido excluídas e todos os registros na tabela de índices.  
  
## <a name="see-also"></a>Consulte também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)
