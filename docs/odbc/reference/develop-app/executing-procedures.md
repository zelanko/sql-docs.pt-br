---
title: Procedimentos de Execução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305707"
---
# <a name="executing-procedures"></a>Executar procedimentos
A ODBC define uma seqüência de fuga padrão para a execução de procedimentos. Para obter a sintaxe desta seqüência e um exemplo de código que a usa, consulte [Chamadas de Procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Para executar um procedimento, um aplicativo executa as seguintes ações:  
  
1.  Define os valores de quaisquer parâmetros. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
2.  Chama **SQLExecDirect** e passa-a uma seqüência contendo a declaração SQL que executa o procedimento. Esta instrução pode usar a seqüência de fuga definida pela sintaxe específica do ODBC ou DBMS; declarações que usam sintaxe específica do DBMS não são interoperáveis.  
  
3.  Quando **o SQLExecDirect** é chamado, o driver:  
  
    -   Recupera os valores atuais do parâmetro e converte-os conforme necessário. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
    -   Chama o procedimento na fonte de dados e envia-lhe os valores do parâmetro convertido. Como o motorista chama o procedimento é específico do motorista. Por exemplo, ele pode modificar a declaração SQL para usar a gramática SQL da fonte de dados e enviar esta declaração para execução, ou pode chamar o procedimento diretamente usando um mecanismo de Chamada de Procedimento Remoto (RPC) definido no protocolo de fluxo de dados do DBMS.  
  
    -   Retorna os valores de quaisquer parâmetros de entrada/saída ou de saída ou do valor de retorno do procedimento, assumindo que o procedimento seja bem sucedido. Esses valores podem não estar disponíveis até que todos os outros resultados (contagem de linhas e conjuntos de resultados) gerados pelo procedimento tenham sido processados. Se o procedimento falhar, o motorista retorna quaisquer erros.
