---
title: Gerar XML de conjuntos de linhas com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 75446ba8c61f03c46c4000793d7ca75f1dc8cb85
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201106"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>Gerar XML de conjuntos de linhas com FOR XML
  Você pode gerar uma `xml` instância de tipo de dados de um conjunto de linhas usando FOR XML com o novo **tipo** diretiva.  
  
 O resultado pode ser atribuído a um `xml` coluna, variável ou parâmetro de tipo de dados. Além disso, o FOR XML pode ser aninhado para gerar qualquer estrutura hierárquica. Isso torna o FOR XML aninhado muito mais conveniente de escrever do que o FOR XML EXPLICIT, mas ele pode não executar tão bem para hierarquias profundas. O FOR XML também introduz um modo de PATH novo. Esse novo modo especifica o caminho na árvore XML onde o valor de uma coluna aparece.  
  
 A nova diretiva **FOR XML TYPE** pode ser usada para definir exibições XML de somente leitura sobre dados relacionais com sintaxe SQL. A exibição pode ser consultada com instruções SQL e XQuery inserido, conforme mostrado no exemplo a seguir. Também é possível fazer referência a essas exibições SQL em procedimentos armazenados.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>Exemplo: Exibição SQL que retorna tipo de dados xml gerado  
 A definição da exibição SQL a seguir cria uma exibição XML sobre uma coluna relacional, pk, e autores de livros recuperados de uma coluna XML:  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 A exibição V contém uma única linha com uma única columnxmlVal de tipo XML`.` ele pode ser consultado como uma `xml` instância de tipo de dados. Por exemplo, a consulta a seguir retorna o autor cujo primeiro nome é "David":  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 As definições da exibição SQL são um pouco semelhantes a exibições XML que são criadas usando esquemas anotados. No entanto há diferenças importantes. A definição da exibição SQL é somente leitura e deve ser manipulada com XQuery inserido. As exibições XML são criadas usando esquema anotado. Além disso, a exibição SQL materializa o resultado XML antes de aplicar a expressão XQuery, enquanto as consultas XPath nas exibições XML avaliam consultas SQL nas tabelas subjacentes.  
  
## <a name="see-also"></a>Consulte também  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
