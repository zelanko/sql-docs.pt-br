---
title: Definir comando excluído | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
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
 (O padrão para o driver; o padrão para o Visual FoxPro é desativado.) Especifica que os comandos que operam em registros (incluindo registros em tabelas relacionadas) usando um escopo ignoram os registros marcados para exclusão.  
  
 OFF  
 Especifica que os registros marcados para exclusão podem ser acessados por comandos que operam em registros (incluindo registros em tabelas relacionadas) usando um escopo.  
  
## <a name="remarks"></a>Comentários  
 As consultas que usam DELETED () para testar o status dos registros podem ser otimizadas usando a tecnologia Rushmore do Visual FoxPro se a tabela for indexada em DELETED ().  
  
> [!IMPORTANT]  
>  SET DELETED será ignorado se o escopo padrão do comando for o registro atual ou se você incluir um escopo de um único registro. O índice sempre ignora o conjunto excluído e indexa todos os registros na tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)
