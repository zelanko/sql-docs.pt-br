---
title: Caracteres inválidos e regras de escape | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 882793b9f35bf1e4d21903464b85c35e70db3234
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="invalid-characters-and-escape-rules"></a>Caracteres inválidos e regras de escape
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como caracteres XML inválidos são tratados pela cláusula FOR XML e lista as regras de escape para caracteres inválidos em nomes XML.  
  
## <a name="for-xml-and-invalid-characters"></a>Para XML e caracteres inválidos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem a entidade definida como caracteres XML inválidos quando eles são retornados dentro de consultas FOR XML que não usam a diretiva TYPE.  
  
 Embora analisadores compatíveis com o XML 1.0 gerem erros de análise independentemente da entidade desses caracteres estarem definidas ou não, o formulário com entidade definida se alinha melhor com XML 1.1. O formulário com entidade definida também potencialmente se alinha melhor com versões futuras do padrão XML. Além disso, ele simplifica a depuração, porque o ponto de código do caractere inválido se torna visível.  
  
 Para usuários de ferramentas XML, nenhuma solução alternativa é necessária, porque o analisador XML falha de qualquer maneira no ponto onde os caracteres inválidos ocorrem no fluxo de dados. Se você usar ferramentas não XML, essa alteração pode exigir que você atualize sua lógica de programação para pesquisar esses caracteres como valores com entidade definida.  
  
 A definição da entidade dos seguintes caracteres de espaço em branco é feita de maneira diferente em consultas FOR XML para preservar sua presença por meio de viagem de ida e volta:  
  
-   Em atributos e conteúdo de elemento: **hex(0D)** (retorno de carro)  
  
-   Em conteúdo de atributo: **hex(09)** (guia), **hex(0A)** (alimentação de linha)  
  
 Esses caracteres são preservados na saída e um analisador não os normalizará.  
  
## <a name="escape-rules"></a>Regras de escape  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nomes que contêm caracteres que são inválidos em nomes XML, como espaços, são convertidos em nomes XML de uma maneira na qual os caracteres inválidos são convertidos em codificação de entidade numérica de escape.  
  
 Há apenas dois caracteres não alfabéticos que podem ocorrer dentro de um nome XML: dois pontos (:) e sublinhado (_). Como o dois pontos já é reservado para namespaces, o sublinhado é escolhido como o caractere de escape. As regras de escape que são usadas para codificação são as seguintes:  
  
-   Qualquer caractere UCS-2 que não seja um caractere de nome XML válido, de acordo com a especificação do XML 1.0, tem o escape feito como _xHHHH\_. O HHHH representa o código UCS-2 hexadecimal de quatro dígitos do caractere na ordem do primeiro bit mais significativo. Por exemplo, o nome da tabela **Order Details** é codificado como Order_x0020_Details.  
  
-   Caracteres que não se ajustam no realm do UCS-2 (as adições de UCS-4 do intervalo de U+00010000 a U+0010FFFF) são codificadas como _xHHHHHHHH\_. O HHHHHHHH representa a codificação UCS-4 hexadecimal de oito dígitos do caractere, se em modo de compatibilidade com versões anteriores do SQL Server 2000. Caso contrário, os caracteres são codificados como _xHHHHHH\_, para se alinharem com o padrão ISO.  
  
-   O caractere de sublinhado não precisa ter escape definido a menos que ele seja seguido pelo caractere x. Por exemplo, o nome da tabela **Order_Details** não é codificado.  
  
-   O dois pontos em identificadores não tem escape definido como um resultado, o elemento namespace e os nomes dos atributos podem ser gerados pela consulta FOR XML. Por exemplo, a consulta a seguir gera um atributo de namespace que tem um dois pontos no nome:  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     A consulta produz este resultado:  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     Observe que WITH XMLNAMESPACES é a maneira recomendada para adicionar namespaces XML.  
  
## <a name="see-also"></a>Consulte Também  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
