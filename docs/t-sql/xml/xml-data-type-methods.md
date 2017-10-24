---
title: "Métodos de tipo de dados XML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcf16bd9b71f27ab91fb02bbfd7bb7625185b44e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-type-methods"></a>Métodos de tipo de dados xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Você pode usar o **xml** métodos para consultar uma instância XML armazenada em uma variável ou coluna de tipo de dados **xml** tipo. Os tópicos nesta seção descrevem como usar o **xml** métodos de tipo de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[consulta &#40; &#41; Método &#40; tipo de dados xml &#41;](../../t-sql/xml/query-method-xml-data-type.md)|Descreve como usar o método query() para consultar uma instância XML.|  
|[valor &#40; &#41; Método &#40; tipo de dados xml &#41;](../../t-sql/xml/value-method-xml-data-type.md)|Descreve como usar o método value() para recuperar um valor do tipo SQL de uma instância XML.|  
|[Existem &#40; &#41; Método &#40; tipo de dados xml &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|Descreve como usar o método exist() para determinar se uma consulta retorna um resultado não vazio.|  
|[Modificar &#40; &#41; Método &#40; tipo de dados xml &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|Descreve como usar o método Modify () para especificar [linguagem de modificação de dados XML &#40; XML DML &#41; ](../../t-sql/xml/xml-data-modification-language-xml-dml.md)instruções para executar atualizações.|  
|[nós &#40; &#41; Método &#40; tipo de dados xml &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|Descreve como usar o método nodes() para rasgar o XML em várias linhas, o que propaga partes de documentos XML em conjuntos de linhas.|  
|[Associando Dados Relacionais Dentro de Dados XML](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|Descreve como associar dados não XML dentro do XML.|  
|[Diretrizes para Usar Métodos de Tipo de Dados XML](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|Descreve diretrizes para usar o **xml** métodos de tipo de dados.|  
  
 Para chamar esses métodos, use a sintaxe de invocação de método de tipo definida pelo usuário. Por exemplo:  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  O **xml** métodos de tipo de dados **Query ()**, **Value ()**, e **exist ()** retornar NULL se forem executados em uma instância XML NULL. Além disso, **Modify ()** não retorna nada, mas **Nodes ()** retorna conjuntos de linhas e um conjunto de linhas vazio com uma entrada NULL.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  

