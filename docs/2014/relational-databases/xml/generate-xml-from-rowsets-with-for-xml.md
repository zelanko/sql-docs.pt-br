---
title: Gerar XML de conjuntos de linhas com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 181d07e187c6b1091d38ebbe0018c61ae856caf3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63204990"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>Gerar XML de conjuntos de linhas com FOR XML
  Você pode gerar uma `xml` instância de tipo de dados por meio de um conjunto de linhas usando for XML com a nova diretiva de **tipo** .  
  
 O resultado pode ser atribuído a uma `xml` coluna, variável ou parâmetro de tipo de dados. Além disso, o FOR XML pode ser aninhado para gerar qualquer estrutura hierárquica. Isso torna o FOR XML aninhado muito mais conveniente de escrever do que o FOR XML EXPLICIT, mas ele pode não executar tão bem para hierarquias profundas. O FOR XML também introduz um modo de PATH novo. Esse novo modo especifica o caminho na árvore XML onde o valor de uma coluna aparece.  
  
 A nova diretiva **FOR XML TYPE** pode ser usada para definir exibições XML de somente leitura sobre dados relacionais com sintaxe SQL. A exibição pode ser consultada com instruções SQL e XQuery inserido, conforme mostrado no exemplo a seguir. Também é possível fazer referência a essas exibições SQL em procedimentos armazenados.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>Exemplo: Exibição SQL que retorna tipo de dados xml gerado  
 A definição da exibição SQL a seguir cria uma exibição XML sobre uma coluna relacional, pk, e autores de livros recuperados de uma coluna XML:  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 A exibição V contém uma única linha com um único columnxmlVal do tipo`.` XML que pode ser consultado como uma instância `xml` de tipo de dados regular. Por exemplo, a consulta a seguir retorna o autor cujo primeiro nome é "David":  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 As definições da exibição SQL são um pouco semelhantes a exibições XML que são criadas usando esquemas anotados. No entanto há diferenças importantes. A definição da exibição SQL é somente leitura e deve ser manipulada com XQuery inserido. As exibições XML são criadas usando esquema anotado. Além disso, a exibição SQL materializa o resultado XML antes de aplicar a expressão XQuery, enquanto as consultas XPath nas exibições XML avaliam consultas SQL nas tabelas subjacentes.  
  
## <a name="see-also"></a>Consulte Também  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
