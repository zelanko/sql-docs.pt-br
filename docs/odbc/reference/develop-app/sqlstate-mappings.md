---
title: Mapeamentos SQLSTATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89be9c958cb848384a67e7eaf74cfecc72f07c35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148878"
---
# <a name="sqlstate-mappings"></a>Mapeamentos de SQLSTATE
Este tópico discute os valores de SQLSTATE para ODBC 2. *x* e o ODBC 3. *x*. Para obter mais informações sobre o ODBC 3. *x* valores SQLSTATE, consulte [apêndice a: Códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 Em ODBC 3. *x*HYxxx SQLSTATEs são retornados em vez de S1xxx e SQLSTATEs 42Sxx são retornados em vez de S00XX. Isso foi feito para alinhar com os padrões ISO e Open Group. Em muitos casos, o mapeamento não é um para um porque os padrões de tem redefinido a interpretação dos vários SQLSTATEs.  
  
 Quando um ODBC 2. *x* aplicativo é atualizado para um ODBC 3. *x* aplicativo, o aplicativo precisa ser alterada para esperar o ODBC 3. *x* SQLSTATEs, em vez de ODBC 2. *x* SQLSTATEs. A tabela a seguir lista o ODBC 3. *x* SQLSTATEs que cada ODBC 2. *x* SQLSTATE é mapeado para.  
  
 Quando o atributo de ambiente SQL_ATTR_ODBC_VERSION é definido como SQL_OV_ODBC2, o driver posta ODBC 2. *x* SQLSTATEs, em vez de ODBC 3. *x* SQLSTATEs quando **SQLGetDiagField** ou **SQLGetDiagRec** é chamado. Um mapeamento específico pode ser determinado, anotando o ODBC 2 *. x* SQLSTATE na coluna 1 da tabela a seguir que corresponde ao ODBC 3. *x* SQLSTATE na coluna 2.  
  
|ODBC 2. *x* SQLSTATE|ODBC 3. *x* SQLSTATE|Comentários|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2. *x* SQLSTATE S1002 é mapeado para o ODBC 3. *x* SQLSTATE 07009 se a função subjacente for **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch** , **SQLFetchScroll**, ou **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Retornado para um uso inválido de um ponteiro nulo.|  
|S1009|HY024|Retornado para um valor de atributo inválido.|  
|S1009|HY092|Retornado para a atualização ou exclusão de dados por uma chamada para **SQLSetPos**, ou adicionando, atualizando ou excluindo dados por uma chamada para **SQLBulkOperations**, quando a simultaneidade é somente leitura.|  
|S1010|HY007 HY010|SQLSTATE S1010 é mapeado para o SQLSTATE HY007 quando **SQLDescribeCol** é chamado antes de chamar **SQLPrepare**, **SQLExecDirect**, ou uma função de catálogo para o *StatementHandle*. Caso contrário, o SQLSTATE S1010 é mapeado para o SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC 3. *x* SQLSTATE 07009 é mapeado para o ODBC 2. *x* SQLSTATE S1093 se a função subjacente for **SQLBindParameter** ou **SQLDescribeParam**.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC 3. *x* SQLSTATE 07008 é mapeado para o ODBC 2. *x* SQLSTATE S1000.
