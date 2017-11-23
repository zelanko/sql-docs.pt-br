---
title: Modify () Method (xml Data Type) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4e84f23554fa43f5163b11fe52d0e0ab97835df9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="modify-method-xml-data-type"></a>Método modifique() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica o conteúdo de um documento XML. Use esse método para modificar o conteúdo de um **xml** coluna ou variável do tipo. Esse método utiliza uma instrução XML DML para inserir, atualizar ou excluir nós de dados XML. O **Modify ()** método o **xml** tipo de dados só pode ser usado na cláusula SET de uma instrução UPDATE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>Argumentos  
 XML_DML  
 É uma cadeia de caracteres em XML DML (linguagem de manipulação de dados). O documento XML é atualizado de acordo com essa expressão.  
  
> [!NOTE]  
>  Um erro será retornado se o **Modify ()** método for chamado em um valor nulo ou resultar em um valor nulo.  
  
## <a name="examples"></a>Exemplos  
 Porque o **Modify ()** método requer uma cadeia de caracteres no XML DML Data Manipulation Language (), os exemplos para **Modify ()** estão contidas nos tópicos que descrevem as instruções XML DML. Para esses exemplos, consulte [insert &#40; XML DML &#41; ](../../t-sql/xml/insert-xml-dml.md), [Excluir &#40; XML DML &#41; ](../../t-sql/xml/delete-xml-dml.md) e [Substituir valor de &#40; XML DML &#41; ](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
