---
title: "Linguagem de modificação de dados XML (XML DML) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5b3315bad83aff77c661edb9e0b3e9e081147d42
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="xml-data-modification-language-xml-dml"></a>Linguagem de modificação de dados XML (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A linguagem de Modificação de Dados XML (XML DML) é uma extensão da linguagem XQuery. Como definido por W3C, a linguagem XQuery é desprovida da parte de Manipulação de Dados (DML). A XML DML apresentada neste tópico, e também a linguagem XQuery, fornece uma consulta totalmente funcional e linguagem de modificação de dados que você pode usar em relação a **xml** tipo de dados.  
  
 A XML DML acrescenta as seguintes palavras-chave que diferenciam maiúsculas e minúsculas à XQuery:  
  
-   **insert**  
  
-   **delete**  
  
-   **Substituir o valor de**  
  
 Conforme descrito em [&#40; tipo de dados XML e colunas SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md), você pode criar variáveis e colunas do **xml** digite e atribuir documentos ou fragmentos XML aos mesmos. Para modificar ou atualizar essas instâncias de XML, faça o seguinte:  
  
-   Use o [tipo de dados do xml de método Modify ())](../../t-sql/xml/modify-method-xml-data-type.md) do **xml** tipo de dados.  
  
-   Especifique as devidas instruções XML DML dentro do **Modify ()** método.  
  
 Observe que há alguns atributos que não podem ser inseridos, excluídos ou ter seus valores modificados. Por exemplo:  
  
-   Para o tipo ou sem-tipo **xml,** os atributos são **xmlns**, **xmlns:\***, e **XML: base**.  
  
-   Para tipo **xml** somente os atributos são **xsi: nil**, e **xsi: Type**.  
  
 Outras restrições incluem o seguinte:  
  
-   Para o tipo ou sem-tipo **xml**, inserindo o atributo **XML: base** falhará.  
  
-   Para tipo **xml**, excluir e modificar o **xsi: nil** atributo falhará. Para não tipados **xml**, você pode excluir o atributo ou modificar seu valor.  
  
-   Para tipo **xml**, modificando o valor da **xs: Type** atributo falhará. Para não tipados **xml**, você pode modificar o valor do atributo.  
  
 Quando você modifica uma instância XML digitada, o formato final deve ser uma instância válida desse tipo. Caso contrário, será retornado um erro de validação.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir &#40; XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [Excluir &#40; XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [Substituir valor de &#40; XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de Tipos de Dados XML](../../t-sql/xml/xml-data-type-methods.md)  
  
  
