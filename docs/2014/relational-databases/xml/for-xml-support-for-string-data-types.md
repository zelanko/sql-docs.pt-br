---
title: Suporte FOR XML para tipos de dados de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f29a28e4b8d6105c84200d0993dbce7b754cbd5
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889154"
---
# <a name="for-xml-support-for-string-data-types"></a>Suporte a FOR XML para tipos de dados de cadeia de caracteres
  O XML gerado pelos caracteres de espaço em branco do FOR XML nos dados tem a entidade definida.  
  
 O exemplo a seguir cria a tabela de exemplo **T** e insere dados de exemplo que incluem caracteres de alimentação de linha, retorno de carro e tabulação. A instrução SELECT recupera os dados da tabela.  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 Este é o resultado:  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O retorno de carro na primeira linha tem a entidade definida como &#xD.  
  
-   O caractere tab na segunda linha tem a entidade definida como &#x09.  
  
-   O caractere de alimentação de linha na terceira linha tem a entidade definida como &#xA.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a FOR XML para vários tipos de dados SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
