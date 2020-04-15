---
title: Papel do Gerente de Motorista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304297"
---
# <a name="role-of-the-driver-manager"></a>Função do Gerenciador do Driver
O Driver Manager determina a ordem final para retornar os registros de status que ele gera. Em particular, determina qual registro tem o mais alto posto e deve ser devolvido primeiro. O motorista é responsável por encomendar registros de status que gera. Se os registros de status forem publicados pelo Driver Manager e pelo motorista, o Driver Manager será responsável por encomendá-los. Para obter mais informações, consulte [Seqüência de Registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 O Driver Manager faz o máximo de verificação de erros que puder. Isso evita que todos os motoristas verifiquem os mesmos erros. Por exemplo, se um argumento de função aceitar um número discreto de valores, como *operação* em **SQLSetPos,** o Gerenciador de driver verifica se o valor especificado é legal.  
  
 As seções a seguir descrevem os tipos de condições verificadas pelo Driver Manager. Eles não se destinam a ser exaustivos; para obter uma lista completa dos SQLSTATEs, o Driver Manager retorna, consulte a seção "Diagnósticos" de cada função; a descrição de cada verificação feita pelo Driver Manager começa com as letras "(DM)." Veja também as tabelas de transição de estado no [apêndice B: Tabelas de Transição do Estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); erros mostrados entre parênteses são detectados pelo Gerenciador de Driver.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Verificações de valor de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Verificações de transição de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Verificações de erro gerais](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Verificações de aviso e de erro do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
