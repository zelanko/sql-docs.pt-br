---
title: Opções de consulta de execução (página ANSI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d9a8b5dea5ab90137c95c9ddaf609c63532dd5b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089075"
---
# <a name="query-options-execution-ansi-page"></a>Execução de Opções de Consulta (página ANSI)
  Use esta página para especificar que o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executará as consultas usando todas ou uma parte das configurações especificadas no padrão ISO (ANSI).  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **SET ANSI_DEFAULTS**  
 Selecione todas as configurações ISO padrão. Essa caixa fica indisponível por padrão, pois só algumas das configurações ISO são feitas.  
  
 **SET QUOTED_IDENTIFIER**  
 Coloque os identificadores de objeto entre aspas. Esta opção é selecionada por padrão.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Permita valores nulos para todos os tipos de dados ou colunas definidos pelo usuário que não estejam explicitamente definidos como NOTNULL durante uma instrução CREATE TABLE ou ALTER TABLE (o estado padrão). Esta opção é selecionada por padrão.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Por padrão, esta opção não é selecionada.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Feche os cursores abertos automaticamente (conforme ISO) quando uma transação for confirmada. Quando apagados (definidos como OFF), os cursores permanecem abertos nos limites da transação, fechando apenas quando a conexão for fechada ou quando eles forem explicitamente fechados. Por padrão, esta opção não é selecionada.  
  
 **SET ANSI_PADDING**  
 Controla como a coluna armazena valores menores que o tamanho definido da coluna e valores com espaços em branco à direita em dados do tipo **char**, **varchar**, **binary**e **varbinary** . Essa configuração afeta somente a definição de novas colunas. Depois que a coluna é criada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazena os valores com base na configuração de quando a coluna foi criada. As colunas existentes não são afetadas por uma alteração posterior a essa configuração. Esta caixa de seleção fica marcada por padrão.  
  
 **SET ANSI_WARNINGS**  
 Especifica o comportamento ISO padrão em várias condições de erro:  
  
-   Quando essa caixa de seleção é marcada, se forem exibidos valores nulos em funções de agregação (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT), será gerada uma mensagem de aviso. Quando **OFF**, nenhum aviso é emitido.  
  
-   Quando essa caixa de seleção é desmarcada, erros de estouro aritmético e de divisão por zero fazem a instrução ser retornada e uma mensagem de erro é gerada. Quando OFF, erros de estouro aritmético e de divisão por zero fazem com que valores nulos sejam retornados. O comportamento em que um erro de estouro aritmético e de divisão por zero faz como que valores nulos sejam retornados ocorre se houver uma tentativa de operação INSERT ou UPDATE em uma coluna de caracteres, Unicode ou binária que tenha novo valor com tamanho maior que o tamanho máximo da coluna. Quando **SET ANSI_WARNINGS** está ON, a operação INSERT ou UPDATE é cancelada, como especificado pelo padrão ISO. Espaços em branco à direita são ignorados em colunas de caracteres e valores nulos à direita são ignorados em colunas binárias. Quando OFF, os dados são truncados para o tamanho da coluna e a instrução obtém êxito.  
  
 Esta opção é selecionada por padrão.  
  
 **SET ANSI_NULLS**  
 Especifica o comportamento compatível com ISO dos operadores de comparação Igual a (`=`) e Diferente de (`<>`) quando usados com valores nulos. Quando **SET ANSI_NULLS** é selecionado, todas as comparações com um valor nulo são avaliadas como UNKNOWN, o comportamento compatível com ISO. Quando **SET ANSI_NULLS** não é selecionado, as comparações de todos os dados com um valor nulo são avaliadas como TRUE se o valor dos dados for NULL. Esta opção é selecionada por padrão.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
