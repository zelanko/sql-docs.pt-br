---
title: Tipos de dados C em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 748347b0a5b20f22cf7191213c59d2879df67522
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118722"
---
# <a name="c-data-types-in-odbc"></a>Tipos de dados do C em ODBC
ODBC define os tipos de dados de C que são usados por variáveis de aplicativo e seus identificadores de tipo correspondente. Eles são usados pelos buffers associados a colunas do conjunto de resultados e parâmetros de instrução. Por exemplo, suponha que um aplicativo quiser recuperar dados de uma coluna do conjunto de resultados em formato de caractere. Ele declara uma variável com o SQLCHAR * tipo de dados e é associado a essa variável para a coluna do conjunto de resultados com um identificador de tipo de SQL_C_CHAR. Para obter uma lista completa de tipos de dados C e identificadores de tipo, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 O ODBC também define um mapeamento de padrão de cada tipo de dados SQL para um tipo de dados C. Por exemplo, um inteiro de 2 bytes na fonte de dados é mapeado para um inteiro de 2 bytes no aplicativo. Para usar o mapeamento padrão, um aplicativo especifica o identificador de tipo SQL_C_DEFAULT. No entanto, o uso desse identificador é recomendado por motivos de interoperabilidade.  
  
 Todos os tipos de dados de inteiro C definidos no ODBC *1.x* foram assinadas. Tipos de dados sem sinal do C e seus identificadores de tipo correspondente foram adicionadas em ODBC 2.0. Por isso, precisam ter cuidado ao lidar com aplicativos e drivers *1.x* versões.  
  
## <a name="c-data-type-extensibility"></a>Extensibilidade do tipo de dados C  
 No ODBC 3.8, você pode especificar os tipos de dados C específicos do driver. Isso permite que você associe um tipo SQL como um tipo de C específicos do driver em aplicativos ODBC quando você chama [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), ou [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Isso pode ser útil para dar suporte a novos tipos de servidor, porque os tipos de dados C existentes podem não representar corretamente os novos tipos de dados do servidor. Usar tipos do C específicos do driver pode aumentar o número de conversões que podem ser executadas por drivers.  
  
 Por exemplo, suponha que um sistema de gerenciamento de banco de dados (DBMS) introduziu um novo tipo de SQL **DATETIMEOFFSET**, para representar a data e hora com informações de fuso horário. Não haveria nenhum tipo específico de C em ODBC que correspondessem à **DATETIMEOFFSET**. Um aplicativo precisa associar **DATETIMEOFFSET** como SQL_C_BINARY e conversão para uma data definida pelo usuário digite. Começando no ODBC 3.8 com extensibilidade do tipo de dados C, um driver pode definir um novo tipo de C correspondente. Por exemplo, para o novo tipo SQL DATETIMEOFFSET, o driver pode definir um novo tipo de C correspondente, como SQL_C_DATETIMEOFFSET. Em seguida, um aplicativo pode associar o novo tipo SQL como um tipo de C específicos do driver.  
  
 Um tipo de dados C é definido no driver da seguinte maneira:  
  
-   O nível de conformidade para um aplicativo, o driver ODBC e o Gerenciador de Driver ODBC é 3,8 (ou superior).  
  
-   O intervalo de dados de um tipo de C específicos do driver está entre 0x4000 e 0x7FFF.  
  
-   O driver define a estrutura dos dados corresponde ao tipo de C.  Isso pode ser feito no SDK específicas do driver.  
  
 O Gerenciador de driver não validará a um tipo de C definido no intervalo de 0x4000 e 0x7FFF; o driver executará a validação e nenhuma conversão de tipos de dados. Mas, se o intervalo de dados de um tipo de C passado para o Gerenciador de driver entre 0x0000 e 0x3FFF ou entre 0x8000 e 0xFFFF, o Gerenciador de driver validará o tipo de dados C.  
  
> [!NOTE]  
>  Tipos de dados C específicos do driver devem ser descritos na documentação do driver.  
  
 Para especificar um nível de compatibilidade de ODBC de 3.8, um aplicativo chama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) o SQL_ATTR_ODBC_VERSION de atributo definido como **SQL_OV_ODBC3_80**. Para determinar a versão do driver, um aplicativo chama **SQLGetInfo** com SQL_DRIVER_ODBC_VER.  
  
 Para obter mais informações sobre o ODBC 3.8, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do C](../../../odbc/reference/appendixes/c-data-types.md)
