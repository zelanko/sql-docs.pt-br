---
title: Suporte FOR XML para tipos de dados de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15f876fde9403d65ba6af81b7038519d4318100f
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665120"
---
# <a name="for-xml-support-for-string-data-types"></a>Suporte a FOR XML para tipos de dados de cadeia de caracteres
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Suporte a FOR XML para vários tipos de dados de SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
