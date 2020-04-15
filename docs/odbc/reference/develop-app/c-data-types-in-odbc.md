---
title: C Tipos de Dados em ODBC | Microsoft Docs
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
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306291"
---
# <a name="c-data-types-in-odbc"></a>Tipos de dados do C em ODBC
O ODBC define os tipos de dados C que são usados por variáveis de aplicação e seus identificadores de tipo correspondentes. Estes são usados pelos buffers que são obrigados a definir colunas de resultados e parâmetros de declaração. Por exemplo, suponha que um aplicativo queira recuperar dados de uma coluna definida por resultados em formato de caractere. Ele declara uma variável com o tipo de dados SQLCHAR * e vincula esta variável à coluna do conjunto de resultados com um identificador de tipo de SQL_C_CHAR. Para obter uma lista completa de tipos de dados C e identificadores de tipo, consulte [Apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 O ODBC também define um mapeamento padrão de cada tipo de dados SQL para um tipo de dados C. Por exemplo, um inteiro de 2 bytes na fonte de dados é mapeado para um inteiro de 2 bytes no aplicativo. Para usar o mapeamento padrão, um aplicativo especifica o identificador de tipo SQL_C_DEFAULT. No entanto, o uso deste identificador é desencorajado por razões de interoperabilidade.  
  
 Todos os tipos de dados inteiros C definidos no ODBC *1.x* foram assinados. Os tipos de dados C não assinados e seus identificadores de tipo correspondentes foram adicionados no ODBC 2.0. Por causa disso, aplicativos e drivers precisam ser particularmente cuidadosos ao lidar com versões *1.x.*  
  
## <a name="c-data-type-extensibility"></a>Extensibilidade do tipo de dados C  
 No ODBC 3.8, você pode especificar os tipos de dados C específicos do driver. Isso permite vincular um tipo SQL como um tipo C específico do driver em aplicativos ODBC quando você chamar [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)ou [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Isso pode ser útil para suportar novos tipos de servidor, porque os tipos de dados C existentes podem não representar corretamente os novos tipos de dados do servidor. Usar tipos C específicos do driver pode aumentar o número de conversões que os motoristas podem realizar.  
  
 Por exemplo, suponha que um sistema de gerenciamento de banco de dados (DBMS) introduziu um novo tipo de SQL, **DATETIMEOFFSET**, para representar a data e a hora com informações de fuso horário. Não haveria um tipo C específico no ODBC que correspondesse ao **DATETIMEOFFSET**. Um aplicativo teria que vincular **DATETIMEOFFSET** como SQL_C_BINARY e lançá-lo a um tipo de dados definido pelo usuário. A partir de ODBC 3.8 com extensibilidade do tipo de dados C, um driver pode definir um novo tipo C correspondente. Por exemplo, para o novo tipo SQL DATETIMEOFFSET, o driver pode definir um novo tipo C correspondente, como SQL_C_DATETIMEOFFSET. Em seguida, um aplicativo pode vincular o novo tipo SQL como um tipo C específico do driver.  
  
 Um tipo de dados C é definido no driver da seguinte forma:  
  
-   O nível de conformidade oDBC para um aplicativo, driver ODBC e Driver Manager é de 3.8 (ou superior).  
  
-   O intervalo de dados de um tipo C específico do driver é entre 0x4000 e 0x7FFF.  
  
-   O driver define a estrutura dos dados correspondentes ao tipo C.  Isso pode ser feito no SDK específico do driver.  
  
 O driver manager não validará um tipo C definido na faixa de 0x4000 e 0x7FFF; o driver realizará a validação e qualquer conversão de tipo de dados. Mas se o intervalo de dados de um tipo C passado para o driver manager é entre 0x0000 e 0x3FFF ou entre 0x8000 e 0xFFFF, o gerente do driver validará o tipo de dados C.  
  
> [!NOTE]  
>  Os tipos de dados C específicos do driver devem ser descritos na documentação do driver.  
  
 Para especificar um nível de conformidade ODBC de 3.8, um aplicativo chama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) com o atributo SQL_ATTR_ODBC_VERSION definido como **SQL_OV_ODBC3_80**. Para determinar a versão do driver, um aplicativo chama **SQLGetInfo** com SQL_DRIVER_ODBC_VER.  
  
 Para obter mais informações sobre o ODBC 3.8, consulte [O que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do C](../../../odbc/reference/appendixes/c-data-types.md)
