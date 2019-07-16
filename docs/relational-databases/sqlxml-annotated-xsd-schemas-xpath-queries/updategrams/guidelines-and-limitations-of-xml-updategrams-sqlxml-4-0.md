---
title: Diretrizes e limitações dos diagramas de atualização XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb8a2a978e70b5148b78f394cf0d8413d5769c64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086850"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>Diretrizes e limitações dos diagramas de atualização XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Lembre-se das recomendações a seguir ao usar diagramas de atualização XML:  
  
-   Se você estiver usando um diagrama de atualização para uma operação de inserção com apenas um único par de  **\<antes de >** e  **\<depois >** blocos, o  **\<antes >** bloco pode ser omitido. Por outro lado, no caso de uma operação de exclusão, o  **\<depois >** bloco pode ser omitido.  
  
-   Se você estiver usando um diagrama de atualização com vários  **\<antes de >** e  **\<depois >** blocos no  **\<sincronização >** marcar, ambos  **\<antes de >** blocos e  **\<depois >** blocos devem ser especificados para o formulário  **\<antes >** e  **\<depois >** pares.  
  
-   As atualizações em um diagrama de atualização são aplicadas à exibição XML fornecida pelo esquema XML. Portanto, para o mapeamento padrão obter êxito em qualquer uma das situações, você precisará especificar o nome do arquivo de esquema no diagrama de atualização ou, se o nome do arquivo não for fornecido, os nomes de elemento e atributo precisarão corresponder aos nomes de tabela e coluna no banco de dados.  
  
-   O SQLXML 4.0 exige que todos os valores de coluna de um diagrama de atualização sejam mapeados explicitamente no esquema (XDR ou XSD) fornecido para compor a exibição XML de seus elementos filho. Esse comportamento é diferente de versões anteriores do SQLXML, que permitiam um valor para uma coluna não mapeada no esquema se fosse sugerido como parte da chave estrangeira em uma **SQL: Relationship** anotação. (Observe que essa alteração não influencia na propagação dos valores de chave primária para os elementos filho, que ainda ocorrerá para o SQLXML 4.0 se nenhum valor for especificado explicitamente para o elemento filho.  
  
-   Se você estiver usando um diagrama de atualização para modificar dados em uma coluna binária (como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **imagem** tipo de dados), você deve fornecer um esquema de mapeamento no qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados (por exemplo, **SQL: DataType = "imagem"** ) e o tipo de dados XML (por exemplo, **dt: type = "binhex"** ou **dt: type = "binbase64**) deve ser especificado. Os dados da coluna binária devem ser especificados no diagrama de atualização; o **SQL: URL-codificar** anotação que é especificada no esquema de mapeamento é ignorada pelo diagrama de atualização.  
  
-   Quando você estiver escrevendo um esquema XSD, se o valor especificado para o **Relation** ou **SQL: Field** anotação inclui um caractere especial, como um caractere de espaço (por exemplo, em "Order Details" nome da tabela), esse valor deve estar entre colchetes (por exemplo, "[Order Details]").  
  
-   Ao usar diagramas de atualização, não são suportadas relações de cadeia. Por exemplo, se as tabelas A e C tiverem uma relação de cadeia que use a tabela B, ocorrerá o erro a seguir ao tentar executar o diagrama de atualização:  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     Mesmo se o esquema e o diagrama de atualização estiverem corretos e devidamente formados, esse erro ocorrerá se houver uma relação de cadeia.  
  
-   Diagramas de atualização não permitem a passagem de **imagem** tipo de dados como parâmetros durante as atualizações.  
  
-   Tipos de objeto binário grande (BLOB), como **texto/ntext** e imagens não devem ser usadas na  **\<antes >** bloquear ao trabalhar com diagramas de atualização, pois isso incluirá para uso em controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do **texto** de tipo de dados; no entanto, as comparações falharão no caso de tipos BLOB onde o tamanho dos dados é maior que 8 KB.  
  
-   Caracteres especiais no **ntext** dados podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" na  **\<antes de >** bloco de um diagrama de atualização quando usado na verificação simultânea de uma coluna de **ntext** tipo falhará com o SQLOLEDB a seguir Descrição do erro:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
