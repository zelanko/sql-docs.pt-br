---
title: Alterações de comportamento e Drivers ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e386aa60489fe3edb2caac3cb49ebad263ffdfac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740044"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Alterações de comportamento e os drivers ODBC 3.x
O atributo de ambiente SQL_ATTR_ODBC_VERSION indica para o driver se ele precisa apresentar ODBC 2. *x* comportamento ou o ODBC 3 *. x* comportamento. Como o atributo de ambiente SQL_ATTR_ODBC_VERSION é definido depende do aplicativo. 3 de ODBC *. x* aplicativos devem chamar **SQLSetEnvAttr** definir esse atributo depois que eles chamam **SQLAllocHandle** para alocar um identificador de ambiente e antes de chamarem  **Falha de SQLAllocHandle** para alocar um identificador de conexão. Se elas não conseguem fazer isso, o Gerenciador de Driver retornará SQLSTATE HY010 (erro de sequência de função) na última chamada para **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obter mais informações sobre alterações de comportamento e como um aplicativo funciona, consulte [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 ODBC 2. *x* aplicativos e o ODBC 2. *x* aplicativos recompilados com o ODBC 3 *. x* arquivos de cabeçalho não chamam **SQLSetEnvAttr**. No entanto, eles chamam **SQLAllocEnv** em vez de **SQLAllocHandle** para alocar um identificador de ambiente. Portanto, quando o aplicativo chama **SQLAllocEnv** no Gerenciador de Driver, o Gerenciador de Driver chama **SQLAllocHandle** e **SQLSetEnvAttr** no driver. Portanto, o ODBC 3 *. x* drivers podem sempre contar com esse atributo que está sendo definido.  
  
 Se um aplicativo compatível com os padrões compilado com o sinalizador de compilação ODBC_STD chamadas **SQLAllocEnv** (que pode ocorrer porque **SQLAllocEnv** não foi preterido no ISO), a chamada é mapeada para  **SQLAllocHandleStd** em tempo de compilação. No tempo de execução, o aplicativo chama **SQLAllocHandleStd**. O Gerenciador de Driver define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** é equivalente a uma chamada para **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3.  
  
 Em determinadas arquiteturas do driver, é necessário para o driver seja exibido como um ODBC 2. *x* driver ou um ODBC 3 *. x* driver, dependendo da conexão. O driver nesse caso, talvez não, na verdade, ser um driver, mas uma camada que reside entre o Gerenciador de Driver e o outro driver. Por exemplo, ele pode imitar um driver, como um espião de ODBC. Em outro exemplo, ele pode atuar como um gateway, como EDA/SQL. Seja exibido como um ODBC 3 *. x* driver, um driver deve ser capaz de exportar **SQLAllocHandle**e seja exibido como um ODBC 2. *x* driver, deve ser capaz de exportar **SQLAllocConnect**, **SQLAllocEnv**, e **SQLAllocStmt**. Quando um ambiente, conexão ou a instrução deve ser alocada, o Gerenciador de Driver verifica para ver se esse driver exporta **SQLAllocHandle**. Uma vez que o driver faz as chamadas de Gerenciador de Driver **SQLAllocHandle** no driver. Se o driver está trabalhando com um ODBC 2. *x* driver, o driver deve mapear a chamada para **SQLAllocHandle** para **SQLAllocConnect**, **SQLAllocEnv**, ou  **SQLAllocStmt**, conforme apropriado. Ele também deve fazer nada com o **SQLSetEnvAttr** chamar quando se comportando como um ODBC 2. *x* driver.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipo de dados datetime](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidade com versões anteriores de tipos de dados do C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Indicadores de comprimento fixo](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Suporte SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Retornando SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Chamando SQLSetPos para inserir dados](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Carregamento por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
