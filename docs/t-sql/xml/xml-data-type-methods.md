---
title: Métodos do tipo de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 715effa0eb16a298f5064f08d2751df07bfa8677
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020208"
---
# <a name="xml-data-type-methods"></a>Métodos de tipo de dados xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Use os métodos do tipo de dados **XML** para consultar uma instância XML armazenada em uma variável ou coluna do tipo **XML**. Os tópicos nesta seção descrevem como usar os métodos do tipo de dados **XML**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Método query&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/query-method-xml-data-type.md)|Descreve como usar o método query() para consultar uma instância XML.|  
|[Método value&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/value-method-xml-data-type.md)|Descreve como usar o método value() para recuperar um valor do tipo SQL de uma instância XML.|  
|[Método exist&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/exist-method-xml-data-type.md)|Descreve como usar o método exist() para determinar se uma consulta retorna um resultado não vazio.|  
|[Método modify&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/modify-method-xml-data-type.md)|Descreve como usar o método Modify() para especificar instruções [XML DML &#40;linguagem de manipulação de dados XML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md) para executar atualizações.|  
|[Métodos nodes&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|Descreve como usar o método nodes() para rasgar o XML em várias linhas, o que propaga partes de documentos XML em conjuntos de linhas.|  
|[Associando Dados Relacionais Dentro de Dados XML](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|Descreve como associar dados não XML dentro do XML.|  
|[Diretrizes para Usar Métodos de Tipo de Dados XML](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|Descreve as diretrizes para usar os métodos do tipo de dados **XML**.|  
  
 Para chamar esses métodos, use a sintaxe de invocação de método de tipo definida pelo usuário. Por exemplo:  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  Os métodos do tipo de dados **XML** **query()**, **value()** e **exist()** retornarão NULL se forem executados em uma instância XML NULL. Além disso, **modify()** não retorna nada, mas **nodes()** retorna conjuntos de linhas e um conjunto de linhas vazio com uma entrada NULL.  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
