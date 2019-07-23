---
title: Usar a opção BINARY BASE64 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d715b1e90c54c549a255b3ee43f24f2e5556d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039164"
---
# <a name="use-the-binary-base64-option"></a>Usar a opção BINARY BASE64
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  A opção BINARY BASE64 é especificada na consulta. Os dados binários são retornados no formato de codificação na base64. Por padrão, se a opção BINARY BASE64 não for especificada, o modo AUTO oferecerá suporte à codificação de URL dos dados binários. Isto é, em vez dos dados binários, uma referência a uma URL relativa à raiz virtual do banco de dados onde a consulta é executada é retornada. Essa referência pode ser usada para acessar os dados binários reais em operações subsequentes usando a consulta dboject SQLXML ISAPI. A consulta deve fornecer informações suficientes, como colunas de chave primária para identificar a imagem.  
  
 Para especificar uma consulta, se um alias for usado para a coluna binária da exibição, o alias será retornado na codificação de URL dos dados binários. Em operações subsequentes, o alias não tem sentido e a codificação de URL não pode ser usada para recuperar a imagem. Portanto não use alias ao consultar uma exibição usando o modo FOR XML AUTO.  
  
 Por exemplo, em uma consulta SELECT, a conversão de qualquer coluna em BLOB (objeto binário grande) o transforma em uma entidade temporária na qual ele perde o nome da tabela associada e o nome da coluna. Isso faz com que as consultas em modo AUTO gerem um erro porque ele não sabe onde colocar esse valor na hierarquia XML. Por exemplo:  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 Esta consulta produz um erro por causa da conversão em um BLOB (objeto binário grande):  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 A solução é adicionar a opção BINARY BASE64 à cláusula FOR XML. Se você remover a conversão, a consulta produzirá os resultados conforme esperado:  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 Este é o resultado:  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
