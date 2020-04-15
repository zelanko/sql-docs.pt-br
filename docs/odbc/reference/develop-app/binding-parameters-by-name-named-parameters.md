---
title: Parâmetros de vinculação por nome (parâmetros nomeados) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306367"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Parâmetros de associação por nome (parâmetros nomeados)
Certos DBMSs permitem que um aplicativo especifique os parâmetros para um procedimento armazenado pelo nome em vez de por posição na chamada do procedimento. Esses parâmetros são chamados *de parâmetros*. O ODBC suporta o uso de parâmetros nomeados. No ODBC, os parâmetros nomeados são usados apenas em chamadas para procedimentos armazenados e não podem ser usados em outras instruções SQL.  
  
 O driver verifica o valor do campo SQL_DESC_UNNAMED do IPD para determinar se os parâmetros nomeados são usados. Se SQL_DESC_UNNAMED não estiver definido para SQL_UNNAMED, o motorista usará o nome no campo SQL_DESC_NAME do IPD para identificar o parâmetro. Para vincular o parâmetro, um aplicativo pode chamar **SQLBindParameter** para especificar as informações do parâmetro e, em seguida, pode chamar **SQLSetDescField** para definir o campo SQL_DESC_NAME do IPD. Quando os parâmetros nomeados são usados, a ordem do parâmetro na chamada do procedimento não é importante e o número de registro do parâmetro é ignorado.  
  
 A diferença entre parâmetros não nomeados e parâmetros nomeados está na relação entre o número recorde do descritor e o número de parâmetros no procedimento. Quando parâmetros não nomeados são usados, o primeiro marcador de parâmetro está relacionado com o primeiro registro no descritor do parâmetro, que por sua vez está relacionado com o primeiro parâmetro (na ordem de criação) na chamada do procedimento. Quando os parâmetros nomeados são utilizados, o primeiro marcador de parâmetro ainda está relacionado com o primeiro registro do descritor do parâmetro, mas a relação entre o número recorde do descritor e o número de parâmetro no procedimento não existe mais. Os parâmetros nomeados não utilizam o mapeamento do número de registro do descritor para a posição do parâmetro do procedimento; em vez disso, o nome do registro do descritor é mapeado para o nome do parâmetro do procedimento.  
  
> [!NOTE]  
>  Se a população automática do IPD estiver habilitada, o driver preencherá o descritor de modo que a ordem dos registros do descritor corresponda à ordem dos parâmetros na definição do procedimento, mesmo se os parâmetros nomeados forem usados.  
  
 Se um parâmetro nomeado for usado, todos os parâmetros devem ser nomeados parâmetros. Se algum parâmetro não for um parâmetro nomeado, então nenhum dos parâmetros ca será nomeado parâmetros. Se houvesse uma mistura de parâmetros nomeados e parâmetros não nomeados, o comportamento seria dependente do motorista.  
  
 Como exemplo de parâmetros nomeados, suponha que um procedimento armazenado no SQL Server tenha sido definido da seguinte forma:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 Neste procedimento, o primeiro @title_idparâmetro, tem um valor padrão de 1. Um aplicativo pode usar o seguinte código para invocar este procedimento de tal forma que ele especifica apenas um parâmetro dinâmico. Este parâmetro é um parâmetro nomeado\@com o nome "citação".  
  
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
