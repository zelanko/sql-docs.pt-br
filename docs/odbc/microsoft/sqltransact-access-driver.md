---
title: SQLTransact (Driver de acesso) | Microsoft Docs
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
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 657d0324132b279300e2a61151c790f066e4a3f5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-access-driver"></a>SQLTransact (Driver de acesso)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de acesso. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Access for usado, SQL_COMMIT e SQL_ROLLBACK têm suporte para o *fType* argumento em uma chamada para **SQLTransact**.  
  
 Se ocorrer uma falha durante o processo de confirmação, o banco de dados afetado pode ser reparado usando a opção Reparar banco de dados na configuração de driver do Microsoft Access ou com o uso da palavra-chave REPAIR_DB no **SQLConfigDataSource** função.

