---
title: Tipos de dados do Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a8385c8efb1ab7dcee651e5acb52062292a0bcc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045020"
---
# <a name="microsoft-excel-data-types"></a>Tipos de dados do Microsoft Excel
A tabela a seguir mostra como os tipos de dados de driver do Microsoft Excel são mapeados para tipos de dados ODBC do SQL. O driver do Microsoft Excel atribui esses tipos de dados a colunas em tabelas do Microsoft Excel com base nos dados na coluna.  
  
|Tipo de dados do Microsoft Excel|Tipo de dados ODBC|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LÓGICO|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados SQL ODBC. Todas as conversões no Apêndice D da *referência do programador de ODBC* têm suporte para os tipos de dados ODBC SQL listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações em tipos de dados do Microsoft Excel.  
  
|Tipo de dados|DESCRIÇÃO|  
|---------------|-----------------|  
|Dados criptografados|O driver do Microsoft Excel não pode ler dados criptografados.|  
|Cadeias de caracteres de erro|O driver do Microsoft Excel não pode retornar uma cadeia de caracteres para os valores de erro do Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? e #NULL!), mas retorna um NULL em vez disso.|  
|LÓGICO|O valor em uma coluna lógica é retornado em um buffer de SQL_C_CHAR como 0 ou 1.|  
|NUMBER|Se uma coluna de inteiro for criada, os números muito grandes para o tipo de dados Integer poderão ser inseridos, e os dados que contêm valores não inteiros poderão ser inseridos, com o resultado de que a coluna pode ser convertida em SQL_DOUBLE.|  
|TEXT|Quando as linhas de uma coluna contêm mais de um tipo de dados do Microsoft Excel, o driver ODBC do Microsoft Excel atribui o tipo de dados SQL_VARCHAR à coluna. Há uma exceção a isso: se a coluna contiver apenas dois ou três dos tipos de dados DateTime (data, hora e DATETIME), o driver ODBC do Microsoft Excel atribuirá o tipo de dados SQL_TIMESTAMP à coluna.<br /><br /> A criação de uma coluna de texto de comprimento zero ou não especificado realmente retorna uma coluna de 255 bytes.<br /><br /> Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (1-255 decimal). Use duas aspas simples consecutivas (") para representar uma aspa simples (').<br /><br /> A inserção de um NULL em uma coluna com um tipo de dados diferente de SQL_VARCHAR fará com que o tipo de dados da coluna seja alterado para SQL_VARCHAR.|  
  
 Mais limitações sobre tipos de dados podem ser encontradas em [limitações de tipo de dados](../../odbc/microsoft/data-type-limitations.md).
