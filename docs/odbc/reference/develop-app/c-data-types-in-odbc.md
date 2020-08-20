---
description: Tipos de dados do C em ODBC
title: Tipos de dados C no ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395f60860dd3179326687a6c2fb10bbaf027ca3a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494756"
---
# <a name="c-data-types-in-odbc"></a>Tipos de dados do C em ODBC
O ODBC define os tipos de dados do C que são usados por variáveis de aplicativo e seus identificadores de tipo correspondentes. Eles são usados pelos buffers associados às colunas do conjunto de resultados e aos parâmetros de instrução. Por exemplo, suponha que um aplicativo queira recuperar dados de uma coluna de conjunto de resultados no formato de caractere. Ele declara uma variável com o tipo de dados SQLCHAR * e associa essa variável à coluna do conjunto de resultados com um identificador de tipo de SQL_C_CHAR. Para obter uma lista completa de tipos de dados C e identificadores de tipo, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 O ODBC também define um mapeamento padrão de cada tipo de dados SQL para um tipo de dados C. Por exemplo, um inteiro de 2 bytes na fonte de dados é mapeado para um inteiro de 2 bytes no aplicativo. Para usar o mapeamento padrão, um aplicativo especifica o identificador de tipo de SQL_C_DEFAULT. No entanto, o uso desse identificador é desencorajado por motivos de interoperabilidade.  
  
 Todos os tipos de dados de inteiro C definidos no ODBC *1. x* foram assinados. Os tipos de dados C não assinados e seus identificadores de tipo correspondentes foram adicionados no ODBC 2,0. Por isso, os aplicativos e os drivers precisam ser especialmente cuidadosos ao lidar com versões *1. x* .  
  
## <a name="c-data-type-extensibility"></a>Extensibilidade de tipo de dados C  
 No ODBC 3,8, você pode especificar tipos de dados C específicos do driver. Isso permite associar um tipo de SQL como um tipo C específico de driver em aplicativos ODBC quando você chama [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)ou [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Isso pode ser útil para dar suporte a novos tipos de servidor, porque os tipos de dados C existentes podem não representar corretamente os novos tipos de dados do servidor. O uso de tipos C específicos de driver pode aumentar o número de conversões que os drivers podem executar.  
  
 Por exemplo, suponha que um DBMS (sistema de gerenciamento de banco de dados) introduziu um novo tipo SQL, **DateTimeOffset**, para representar a data e a hora com informações de fuso horário. Não haveria nenhum tipo C específico em ODBC que correspondesse a **DateTimeOffset**. Um aplicativo teria que associar **DateTimeOffset** como SQL_C_BINARY e convertê-lo em um tipo de dados definido pelo usuário. A partir do ODBC 3,8 com a extensibilidade de tipo de dados C, um driver pode definir um novo tipo C correspondente. Por exemplo, para o novo tipo SQL DATETIMEOFFSET, o driver pode definir um novo tipo C correspondente, como SQL_C_DATETIMEOFFSET. Em seguida, um aplicativo pode associar o novo tipo de SQL como um tipo C específico de driver.  
  
 Um tipo de dados C é definido no driver da seguinte maneira:  
  
-   O nível de conformidade ODBC para um aplicativo, driver ODBC e Gerenciador de driver é 3,8 (ou superior).  
  
-   O intervalo de dados de um tipo C específico de driver é entre 0x4000 e 0x7FFF.  
  
-   O driver define a estrutura dos dados correspondentes ao tipo C.  Isso pode ser feito no SDK específico do driver.  
  
 O Gerenciador de driver não validará um tipo C definido no intervalo de 0x4000 e 0x7FFF; o driver executará a validação e qualquer conversão de tipo de dados. Mas se o intervalo de dados de um tipo C passado para o Gerenciador de driver estiver entre 0x0000 e 0x3FFF ou entre 0x8000 e 0xFFFF, o Gerenciador de Driver validará o tipo de dados C.  
  
> [!NOTE]  
>  Os tipos de dados C específicos do driver devem ser descritos na documentação do driver.  
  
 Para especificar um nível de conformidade ODBC de 3,8, um aplicativo chama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) com o atributo SQL_ATTR_ODBC_VERSION definido como **SQL_OV_ODBC3_80**. Para determinar a versão do driver, um aplicativo chama **SQLGetInfo** com SQL_DRIVER_ODBC_VER.  
  
 Para obter mais informações sobre o ODBC 3,8, consulte [What ' s New in odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do C](../../../odbc/reference/appendixes/c-data-types.md)
