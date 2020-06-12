---
title: Execução de opções de consulta (página ANSI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b20ab1851d02e493035414dd4682fc5330296b19
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83858618"
---
# <a name="query-options-execution-ansi-page"></a>Execução de Opções de Consulta (página ANSI)
  Use esta página para especificar que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o executará as consultas usando todas ou uma parte das configurações especificadas no padrão ISO (ANSI).  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **SET ANSI_DEFAULTS**  
 Selecione todas as configurações ISO padrão. Essa caixa fica indisponível por padrão, pois só algumas das configurações ISO são feitas.  
  
 **SET QUOTED_IDENTIFIER**  
 Coloque os identificadores de objeto entre aspas. Essa opção é habilitada por padrão.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Permita valores nulos para todos os tipos de dados ou colunas definidos pelo usuário que não estejam explicitamente definidos como NOTNULL durante uma instrução CREATE TABLE ou ALTER TABLE (o estado padrão). Essa opção é habilitada por padrão.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Por padrão, esta opção não é selecionada.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Feche os cursores abertos automaticamente (conforme ISO) quando uma transação for confirmada. Quando apagados (definidos como OFF), os cursores permanecem abertos nos limites da transação, fechando apenas quando a conexão for fechada ou quando eles forem explicitamente fechados. Por padrão, esta opção não é selecionada.  
  
 **SET ANSI_PADDING**  
 Controla a maneira como a coluna armazena valores menores do que o tamanho definido da coluna e a maneira como a coluna armazena valores que têm espaços em branco à direita nos dados **Char**, **varchar**, **Binary**e **varbinary** . Essa configuração afeta somente a definição de novas colunas. Depois que a coluna é criada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazena os valores com base na configuração de quando a coluna foi criada. As colunas existentes não são afetadas por uma alteração posterior a essa configuração. Esta caixa de seleção fica marcada por padrão.  
  
 **SET ANSI_WARNINGS**  
 Especifica o comportamento ISO padrão em várias condições de erro:  
  
-   Quando essa caixa de seleção é marcada, se forem exibidos valores nulos em funções de agregação (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT), será gerada uma mensagem de aviso. Quando **desativado**, nenhum aviso é emitido.  
  
-   Quando essa caixa de seleção é desmarcada, erros de estouro aritmético e de divisão por zero fazem a instrução ser retornada e uma mensagem de erro é gerada. Quando OFF, erros de estouro aritmético e de divisão por zero fazem com que valores nulos sejam retornados. O comportamento em que um erro de estouro aritmético e de divisão por zero faz como que valores nulos sejam retornados ocorre se houver uma tentativa de operação INSERT ou UPDATE em uma coluna de caracteres, Unicode ou binária que tenha novo valor com tamanho maior que o tamanho máximo da coluna. Se **SET ANSI_WARNINGS** for on, a operação INSERT ou Update será cancelada conforme especificado pelo padrão ISO. Espaços em branco à direita são ignorados em colunas de caracteres e valores nulos à direita são ignorados em colunas binárias. Quando OFF, os dados são truncados para o tamanho da coluna e a instrução obtém êxito.  
  
 Essa opção é habilitada por padrão.  
  
 **SET ANSI_NULLS**  
 Especifica o comportamento compatível com ISO dos operadores de comparação Igual a (`=`) e Diferente de (`<>`) quando usados com valores nulos. Quando **SET ANSI_NULLS** é selecionado, todas as comparações com um valor nulo são avaliadas como UNKNOWN, o comportamento compatível com ISO. Quando **SET ANSI_NULLS** não é selecionado, as comparações de todos os dados com um valor nulo são avaliadas como TRUE se o valor dos dados for NULL. Essa opção é habilitada por padrão.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
