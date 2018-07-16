---
title: Opção de configuração de servidor transform noise words | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
caps.latest.revision: 43
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 708333809439bcada782b72ce67890dc7b3d5799
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231936"
---
# <a name="transform-noise-words-server-configuration-option"></a>Opção de configuração de servidor para transformar palavras de ruído
  Use o `transform noise words` opção de configuração do servidor para suprimir uma mensagem de erro se palavras de ruído, ou seja [palavras irrelevantes](../../relational-databases/search/full-text-search.md), fazer com que uma operação booliana em uma consulta de texto completo a retornar zero linhas. Essa opção é útil para consultas de texto completo que usam o predicado CONTAINS em que as operações boolianas ou operações NEAR incluem palavras de ruído. Os valores possíveis são descritos na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|0|As palavras de ruído (ou palavras irrelevantes) não são transformadas. Quando uma consulta de texto completo contiver palavras de ruído, a consulta não retornará nenhuma linha e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um aviso. Esse é o comportamento padrão.<br /><br /> Observe que o aviso é um aviso de tempo de execução. Portanto, se a cláusula de texto completo na consulta não for executada, o aviso não será gerado. Para uma consulta local, apenas um aviso é gerado, mesmo quando há várias cláusulas de consulta de texto completo. Para uma consulta remota, o servidor vinculado pode não retransmitir o erro; portanto, o aviso pode não ser gerado.|  
|1|As palavras de ruído (ou palavras irrelevantes) são transformadas. Elas são ignoradas e o resto da consulta é avaliado.<br /><br /> Se forem especificadas palavras de ruído em uma condição de proximidade, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as removerá. Por exemplo, a palavra de ruído `is` é removida de `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`, transformando a consulta de pesquisa em `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`. Observe que `CONTAINS(<column_name>, 'NEAR(hello,is)')` seria transformada simplesmente em `CONTAINS(<column_name>, hello)` porque há apenas um termo de pesquisa válido.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Efeitos da Configuração transformar palavras de ruído  
 Esta seção ilustra o comportamento de consultas que contêm uma palavra de ruído "`the`", nas configurações alternativas de `transform noise words`.  Parte-se do pressuposto de que as cadeias de consulta de texto completo de exemplo são executadas em uma linha de tabela que contém os seguintes dados: `[1, "The black cat"]`.  
  
> [!NOTE]  
>  Todos esses cenários podem gerar um aviso de palavra de ruído.  
  
-   Com transformar palavras de ruído definido como 0:  
  
    |Cadeia de caracteres de consulta|Resultado|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Nenhum resultado (O comportamento é o mesmo para "`the`" AND "`cat`".)|  
    |"`cat`" NEAR "`the`"|Nenhum resultado (O comportamento é o mesmo para "`the`" NEAR "`cat`".)|  
    |"`the`" AND NOT "`black`"|Nenhum resultado|  
    |"`black`" AND NOT "`the`"|Nenhum resultado|  
  
-   Com transformar palavras de ruído definido como 1:  
  
    |Cadeia de caracteres de consulta|Resultado|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Ocorrência da linha com ID 1|  
    |"`cat`" NEAR "`the`"|Ocorrência da linha com ID 1|  
    |"`the`" AND NOT "`black`"|Nenhum resultado|  
    |"`black`" AND NOT "`the`"|Ocorrência da linha com ID 1|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir define `transform noise words` como `1`.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
