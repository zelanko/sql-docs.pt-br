---
title: "Função do Gerenciador de Driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 70c6dba19353cc503dc42b33640c18c4ee72caa9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="role-of-the-driver-manager"></a>Função do Gerenciador de Driver
O Gerenciador de Driver determina a ordem final para retornar registros de status que ele gera. Em particular, ele determina qual registro tem a classificação mais alta e deve ser retornada pela primeira vez. O driver é responsável por ordenar registros de status que ele gera. Se os registros de status são lançados pelo Gerenciador de Driver e o driver, o Gerenciador de Driver é responsável por ordená-los. Para obter mais informações, consulte [sequência de registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 O Gerenciador de Driver não tanta verificação de erro possível. Isso evita que todos os drivers verificando os mesmos erros. Por exemplo, se um argumento de função aceita um número discreto de valores, tais como *operação* na **SQLSetPos**, o Gerenciador de Driver verifica se o valor especificado é válido.  
  
 As seções a seguir descrevem os tipos de condições verificadas pelo Gerenciador de Driver. Eles não se destina a ser completa; Para obter uma lista completa de SQLSTATEs retorna o Gerenciador de Driver, consulte a seção "Diagnóstico" de cada função. a descrição de cada verificação feita pelo Gerenciador de Driver começa com as letras "(DM)". Consulte também as tabelas de transição de estado no [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); erros mostrados entre parênteses são detectados pelo Gerenciador de Driver.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Verificações de valor de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Verificações de transição de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Verificações de erro gerais](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Verificações de aviso e de erro do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

