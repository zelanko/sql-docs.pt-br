---
title: Diretrizes e limitações dos diagramas de atualização XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0e4def47b8e6a7c235f8f80d5be03112ac42d07a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117841"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Diretrizes e limitações dos diagramas de atualização XML (SQLXML 4.0)
  Lembre-se das recomendações a seguir ao usar diagramas de atualização XML:  
  
-   Se você estiver usando um diagrama de atualização para uma operação de inserção com apenas um único par de  **\<antes >** e  **\<depois >** blocos, o  **\<antes >** bloco pode ser omitido. Por outro lado, no caso de uma operação de exclusão, o  **\<depois >** bloco pode ser omitido.  
  
-   Se você estiver usando um diagrama de atualização com vários  **\<antes >** e  **\<depois >** blocos no  **\<sincronização >** marca, ambos  **\<antes >** blocos e  **\<depois >** blocos devem ser especificados para o formulário  **\<antes >** e  **\<depois >** pares.  
  
-   As atualizações em um diagrama de atualização são aplicadas à exibição XML fornecida pelo esquema XML. Portanto, para o mapeamento padrão obter êxito em qualquer uma das situações, você precisará especificar o nome do arquivo de esquema no diagrama de atualização ou, se o nome do arquivo não for fornecido, os nomes de elemento e atributo precisarão corresponder aos nomes de tabela e coluna no banco de dados.  
  
-   O SQLXML 4.0 exige que todos os valores de coluna de um diagrama de atualização sejam mapeados explicitamente no esquema (XDR ou XSD) fornecido para compor a exibição XML de seus elementos filho. Esse comportamento é diferente daquele das versões anteriores do SQLXML, que permitiam um valor para uma coluna não mapeada no esquema se fosse sugerido como parte da Chave estrangeira em uma anotação `sql:relationship`. (Observe que essa alteração não influencia na propagação dos valores de chave primária para os elementos filho, que ainda ocorrerá para o SQLXML 4.0 se nenhum valor for especificado explicitamente para o elemento filho.  
  
-   Se você estiver usando um diagrama de atualização para modificar dados em uma coluna binária (como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `image` tipo de dados), você deve fornecer um esquema de mapeamento no qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados (por exemplo, `sql:datatype="image"`) e o tipo de dados XML (por exemplo, `dt:type="binhex"`ou `dt:type="binbase64`) deve ser especificado. Os dados da coluna binária precisam ser especificados no diagrama de atualização; a anotação `sql:url-encode` especificada no esquema de mapeamento é ignorada pelo diagrama de atualização.  
  
-   Quando você está escrevendo um esquema XSD, se o valor especificado para a anotação `sql:relation` ou `sql:field` incluir um caractere especial, como um caractere de espaço (por exemplo, no nome de tabela "Order Details"), esse valor precisará ser colocado entre colchetes (por exemplo, "[Order Details]").  
  
-   Ao usar diagramas de atualização, não são suportadas relações de cadeia. Por exemplo, se as tabelas A e C tiverem uma relação de cadeia que use a tabela B, ocorrerá o erro a seguir ao tentar executar o diagrama de atualização:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Mesmo se o esquema e o diagrama de atualização estiverem corretos e devidamente formados, esse erro ocorrerá se houver uma relação de cadeia.  
  
-   Os diagramas de atualização não permitem a passagem de dados de tipo `image` como parâmetros durante as atualizações.  
  
-   Tipos de objeto binário grande (BLOB) como `text/ntext` e imagens não devem ser usadas no  **\<antes >** bloco em ao trabalhar com diagramas de atualização, pois isso incluirá para uso em controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do tipo de dados `text`; entretanto, as comparações falharão no caso de tipos BLOB em que o tamanho dos dados seja maior do que 8KB.  
  
-   Caracteres especiais em dados `ntext` podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" no  **\<antes >** bloco de um diagrama de atualização quando usado na verificação simultânea de uma coluna de `ntext` tipo falhará com a descrição de erro SQLOLEDB a seguir:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  