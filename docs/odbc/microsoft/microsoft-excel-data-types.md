---
title: Tipos de dados do Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 204c507e42a429a098c480605da697a6a095f27e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-excel-data-types"></a>Tipos de dados do Microsoft Excel
A tabela a seguir mostra como os tipos de dados de driver do Microsoft Excel são mapeados para tipos de dados SQL ODBC. O driver do Microsoft Excel atribui esses tipos de dados a colunas em tabelas do Microsoft Excel com base nos dados da coluna.  
  
|Tipo de dados do Microsoft Excel|Tipo de dados ODBC|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LÓGICA|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D do *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações nos tipos de dados do Microsoft Excel.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|Dados criptografados|O driver do Microsoft Excel não pode ler os dados criptografados.|  
|Cadeias de caracteres de erro|O driver do Microsoft Excel não pode retornar uma cadeia de caracteres para os valores de erro do Microsoft Excel (# n/d!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? e #NULL!), mas retorna um valor nulo em vez disso.|  
|LÓGICA|O valor em uma coluna lógica é retornado em um buffer SQL_C_CHAR como 0 ou 1.|  
|NUMBER|Se uma coluna de inteiro é criada, números são muito grandes para o tipo de dados inteiro podem ser inseridos e dados que contém valores não inteiros podem ser inseridos, com o resultado que a coluna pode ser convertida em SQL_DOUBLE.|  
|TEXT|Quando as linhas de uma coluna contiverem mais de um tipo de dados do Microsoft Excel, o driver ODBC Microsoft Excel atribuirá o tipo de dados SQL_VARCHAR à coluna. Há uma exceção a isso: se a coluna contiver apenas duas ou três dos tipos de dados de data e hora (data, hora e data e hora), o driver ODBC Microsoft Excel atribuirá o tipo de dados SQL_TIMESTAMP à coluna.<br /><br /> Criação de uma coluna de texto de zero ou comprimento especificado, na verdade, retorna uma coluna de 255 bytes.<br /><br /> Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (decimal de 1 a 255). Use duas aspas simples consecutivas (") para representar uma aspa simples (').<br /><br /> Inserindo um valor nulo em uma coluna com um tipo de dados que não sejam SQL_VARCHAR fará com que o tipo de dados da coluna para alterar para SQL_VARCHAR.|  
  
 Mais limitações nos tipos de dados podem ser encontradas no [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
