---
title: Ligando parâmetros por nome (parâmetros nomeados) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306367"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Parâmetros de associação por nome (parâmetros nomeados)
Determinados DBMSs permitem que um aplicativo especifique os parâmetros para um procedimento armazenado pelo nome, em vez de por posição na chamada de procedimento. Esses parâmetros são chamados de *parâmetros nomeados*. O ODBC dá suporte ao uso de parâmetros nomeados. No ODBC, os parâmetros nomeados são usados somente em chamadas para procedimentos armazenados e não podem ser usados em outras instruções SQL.  
  
 O driver verifica o valor do campo SQL_DESC_UNNAMED do IPD para determinar se os parâmetros nomeados são usados. Se SQL_DESC_UNNAMED não estiver definido como SQL_UNNAMED, o driver usará o nome no campo SQL_DESC_NAME do IPD para identificar o parâmetro. Para associar o parâmetro, um aplicativo pode chamar **SQLBindParameter** para especificar as informações do parâmetro e, em seguida, pode chamar **SQLSetDescField** para definir o campo SQL_DESC_NAME do IPD. Quando parâmetros nomeados são usados, a ordem do parâmetro na chamada de procedimento não é importante e o número do registro do parâmetro é ignorado.  
  
 A diferença entre parâmetros de nome e parâmetros nomeados está na relação entre o número de registro do descritor e o número do parâmetro no procedimento. Quando parâmetros não nomeados são usados, o primeiro marcador de parâmetro está relacionado ao primeiro registro no descritor de parâmetro que, por sua vez, está relacionado ao primeiro parâmetro (na ordem de criação) na chamada de procedimento. Quando parâmetros nomeados são usados, o primeiro marcador de parâmetro ainda está relacionado ao primeiro registro do descritor de parâmetro, mas a relação entre o número de registro do descritor e o número de parâmetro no procedimento não existe mais. Os parâmetros nomeados não usam o mapeamento do número de registro do descritor para a posição do parâmetro de procedimento; em vez disso, o nome do registro do descritor é mapeado para o nome do parâmetro de procedimento.  
  
> [!NOTE]  
>  Se a população automática do IPD estiver habilitada, o driver preencherá o descritor de modo que a ordem dos registros do descritor corresponderá à ordem dos parâmetros na definição do procedimento, mesmo se os parâmetros nomeados forem usados.  
  
 Se um parâmetro nomeado for usado, todos os parâmetros deverão ser nomeados como parâmetros. Se qualquer parâmetro não for um parâmetro nomeado, nenhum dos parâmetros da autoridade de certificação será chamado de parâmetros. Se houver uma mistura de parâmetros nomeados e parâmetros não nomeados, o comportamento seria dependente de driver.  
  
 Como um exemplo de parâmetros nomeados, suponha que um procedimento armazenado SQL Server tenha sido definido da seguinte maneira:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 Neste procedimento, o primeiro parâmetro, @title_id, tem um valor padrão de 1. Um aplicativo pode usar o código a seguir para invocar esse procedimento de modo que ele especifique apenas um parâmetro dinâmico. Esse parâmetro é um parâmetro nomeado com o nome "\@quote".  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
