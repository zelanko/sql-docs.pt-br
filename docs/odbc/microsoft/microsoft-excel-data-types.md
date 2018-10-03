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
manager: craigg
ms.openlocfilehash: 10695dd9bf044e270bb1ce1d26de78e53a1dd85a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656754"
---
# <a name="microsoft-excel-data-types"></a>Tipos de dados do Microsoft Excel
A tabela a seguir mostra como os tipos de dados de driver do Microsoft Excel são mapeados para tipos de dados SQL ODBC. O driver do Microsoft Excel atribui esses tipos de dados a colunas nas tabelas do Microsoft Excel com base nos dados da coluna.  
  
|Tipo de dados do Microsoft Excel|Tipo de dados ODBC|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LÓGICA|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados de ODBC SQL. Todas as conversões no Apêndice D dos *referência do programador de ODBC* têm suporte para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra as limitações nos tipos de dados do Microsoft Excel.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|Dados criptografados|O driver do Microsoft Excel não é possível ler os dados criptografados.|  
|Cadeias de caracteres de erro|O driver do Microsoft Excel não pode retornar uma cadeia de caracteres para os valores de erro do Microsoft Excel (# n/a!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? e #NULL!), mas retorna um valor nulo em vez disso.|  
|LÓGICA|O valor em uma coluna de lógica é retornado em um buffer SQL_C_CHAR como 0 ou 1.|  
|NUMBER|Se for criada uma coluna de inteiros, números que são grandes demais para o tipo de dados inteiro podem ser inseridos e dados que contêm valores não inteiros podem ser inseridos, com o resultado que a coluna pode ser convertida em SQL_DOUBLE.|  
|TEXT|Quando as linhas de uma coluna contiverem mais de um tipo de dados do Microsoft Excel, o driver ODBC Microsoft Excel atribuirá o tipo de dados SQL_VARCHAR à coluna. Há uma exceção a isso: se a coluna contiver apenas duas ou três dos tipos de dados de data e hora (data, hora e data e hora), o driver ODBC Microsoft Excel atribuirá o tipo de dados SQL_TIMESTAMP à coluna.<br /><br /> Criação de uma coluna de texto de zero ou comprimento não especificado, na verdade, retorna uma coluna de 255 bytes.<br /><br /> Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (1 a 255 decimal). Use duas aspas simples consecutivas (") para representar uma marca de aspas simples (').<br /><br /> Inserindo um valor nulo em uma coluna com um tipo de dados que não seja SQL_VARCHAR fará com que o tipo de dados da coluna para alterar para SQL_VARCHAR.|  
  
 Mais limitações nos tipos de dados podem ser encontradas na [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
