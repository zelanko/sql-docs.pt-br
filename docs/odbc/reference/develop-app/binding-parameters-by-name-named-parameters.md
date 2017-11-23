---
title: "Associando parâmetros por nome (parâmetros nomeados) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54298b1c08235452f5717888754569d55442a47a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameters-by-name-named-parameters"></a>Associando parâmetros por nome (parâmetros nomeados)
Determinados DBMSs permitir que um aplicativo especificar os parâmetros para um procedimento armazenado por nome em vez de por posição na chamada de procedimento. Esses parâmetros são chamados *parâmetros nomeados*. ODBC oferece suporte ao uso de parâmetros nomeados. No ODBC, os parâmetros nomeados são usados somente em chamadas para procedimentos armazenados em não podem ser usados em outras instruções SQL.  
  
 O driver verifica o valor do campo SQL_DESC_UNNAMED do IPD para determinar se a chamada parâmetros são usados. Se SQL_DESC_UNNAMED não está definido como SQL_UNNAMED, o driver usa o nome do campo SQL_DESC_NAME do IPD para identificar o parâmetro. Para associar o parâmetro, um aplicativo pode chamar **SQLBindParameter** para especificar as informações de parâmetro e, em seguida, pode chamar **SQLSetDescField** para definir o campo SQL_DESC_NAME do IPD. Quando são usados parâmetros nomeados, a ordem do parâmetro na chamada de procedimento não é importante e o número de registro do parâmetro é ignorado.  
  
 É a diferença entre os parâmetros não nomeados e parâmetros nomeados na relação entre o número do registro do descritor e o número do parâmetro no procedimento. Quando são usados parâmetros sem nome, o primeiro marcador de parâmetro está relacionado para o primeiro registro no descritor de parâmetro, que por sua vez, está relacionado ao primeiro parâmetro (em ordem de criação) na chamada de procedimento. Quando são usados parâmetros nomeados, o primeiro marcador de parâmetro ainda está relacionado para o primeiro registro do descritor de parâmetro, mas a relação entre o número do registro do descritor e o número do parâmetro no procedimento não existe mais. Parâmetros nomeados não usam o mapeamento do número de registros de descritor para a posição de parâmetro de procedimento; em vez disso, o nome de registro do descritor é mapeado para o nome do parâmetro de procedimento.  
  
> [!NOTE]  
>  Se o preenchimento automático do IPD estiver habilitado, o driver preencherá o descritor de modo que a ordem dos registros de descritor corresponderá a ordem dos parâmetros na definição do procedimento, mesmo se forem usados parâmetros nomeados.  
  
 Se um parâmetro nomeado for usado, todos os parâmetros devem ser parâmetros nomeados. Se qualquer parâmetro não é um parâmetro nomeado, em seguida, nenhum dos parâmetros de autoridade de certificação ser parâmetros nomeados. Se houver uma combinação de parâmetros nomeados e parâmetros sem nome, o comportamento seria dependente do driver.  
  
 Como um exemplo de parâmetros nomeados, suponha que um SQL Server que o procedimento armazenado foi definido da seguinte maneira:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 Neste procedimento, o primeiro parâmetro, @title_id, tem um valor padrão de 1. Um aplicativo pode usar o seguinte código para chamar esse procedimento, de modo que ele especifica apenas um parâmetro dinâmico. Esse parâmetro é um parâmetro nomeado com o nome "@quote".  
  
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
