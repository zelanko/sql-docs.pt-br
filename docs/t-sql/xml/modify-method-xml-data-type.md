---
title: Método modify() (tipo de dados xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0c9866d90a532314c75ed65db9fbb0f6e764029
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708504"
---
# <a name="modify-method-xml-data-type"></a>Método modifique() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica o conteúdo de um documento XML. Use esse método para modificar o conteúdo de uma coluna ou variável do tipo **xml**. Esse método utiliza uma instrução XML DML para inserir, atualizar ou excluir nós de dados XML. O método **modify()** do tipo de dados **xml** pode ser usado apenas na cláusula SET de uma instrução UPDATE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>Argumentos  
 XML_DML  
 É uma cadeia de caracteres em XML DML (linguagem de manipulação de dados). O documento XML é atualizado de acordo com essa expressão.  
  
> [!NOTE]  
>  Um erro será retornado se o método **modify()** for chamado em um valor nulo ou resultar em valor nulo.  
  
## <a name="examples"></a>Exemplos  
 Como o método **modify()** exige uma cadeia de caracteres em XML DML (Linguagem de Manipulação de Dados), os exemplos para **modify()** estão contidos nos tópicos que descrevem as instruções XML DML. Para obter esses exemplos, consulte [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md), [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) e [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
