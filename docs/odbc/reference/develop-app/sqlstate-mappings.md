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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec58c0e41869529bbba5fd31ad534976923a990d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299736"
---
# <a name="sqlstate-mappings"></a>Mapeamentos de SQLSTATE
Este tópico discute os valores SQLSTATE para ODBC *2. x* e ODBC *3. x*. Para obter mais informações sobre valores SQLSTATE ODBC *3. x* , consulte [o apêndice A: códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 No ODBC *3. x*, HYXXX sqlstates são retornados em vez de S1xxx, e 42SXX sqlstates são retornados em vez de S00XX. Isso foi feito para se alinhar com os padrões de grupo aberto e ISO. Em muitos casos, o mapeamento não é um-para-um porque os padrões redefiniram a interpretação de vários sqlstates.  
  
 Quando um aplicativo ODBC *2. x* é atualizado para um aplicativo ODBC *3. x* , o aplicativo precisa ser alterado para esperar o ODBC *3. x* sqlstates em vez dos sqlstates do ODBC *2. x* . A tabela a seguir lista os hiperestados ODBC *3. x* para os quais cada ODBC *2. x* SQLSTATE está mapeado.  
  
 Quando o atributo de ambiente SQL_ATTR_ODBC_VERSION é definido como SQL_OV_ODBC2, o driver posta o ODBC *2. x* sqlstates em vez de ODBC *3. x* sqlstates quando **SQLGetDiagField** ou **SQLGetDiagRec** é chamado. Um mapeamento específico pode ser determinado observando-se o SQLSTATE do ODBC *2. x* na coluna 1 da tabela a seguir que corresponde ao SQLSTATE do ODBC *3. x* na coluna 2.  
  
|O ODBC *2. x* SQLSTATE|SQLSTATE ODBC *3. x*|Comentários|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24.000|07005||  
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
|S1002|07009|ODBC *2. x* SQLSTATE S1002 é MAPEADO para ODBC *3. x* SQLSTATE 07009 se a função subjacente for **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**, **SQLFetchScroll**ou **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Retornado para um uso inválido de um ponteiro NULL.|  
|S1009|HY024|Retornado para um valor de atributo inválido.|  
|S1009|HY092|Retornado para atualizar ou excluir dados por uma chamada para **SQLSetPos**, ou adicionar, atualizar ou excluir dados por uma chamada para **SQLBulkOperations**, quando a simultaneidade é somente leitura.|  
|S1010|HY007 HY010|O SQLSTATE S1010 é mapeado para SQLSTATE HY007 quando **SQLDescribeCol** é chamado antes de chamar **SQLPrepare**, **SQLExecDirect**ou uma função de catálogo para o *StatementHandle*. Caso contrário, SQLSTATE S1010 será mapeado para SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|O ODBC *3. x* SQLSTATE 07009 é MAPEADO para ODBC *2. x* SQLSTATE S1093 se a função subjacente for **SQLBindParameter** ou **SQLDescribeParam**.|  
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
>  O ODBC *3. x* SQLSTATE 07008 é MAPEADO para ODBC *2. x* SQLSTATE S1000.
