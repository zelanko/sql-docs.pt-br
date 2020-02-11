---
title: Alterações comportamentais e drivers ODBC 3. x | Microsoft Docs
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
ms.openlocfilehash: 27b48951c6fb3be8bfe070863409d77ab760d5fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915612"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Alterações de comportamento e os drivers ODBC 3.x
O atributo de ambiente SQL_ATTR_ODBC_VERSION indica ao driver se ele precisa exibir o comportamento ODBC *2. x* ou o comportamento ODBC *3. x* . Como o atributo de ambiente SQL_ATTR_ODBC_VERSION é definido depende do aplicativo. Os aplicativos ODBC *3. x* devem chamar **SQLSetEnvAttr** para definir esse atributo depois de chamarem **SQLAllocHandle** para alocar um identificador de ambiente e antes que eles chamem **SQLAllocHandle** para alocar um identificador de conexão. Se eles não conseguirem fazer isso, o Gerenciador de driver retornará SQLSTATE HY010 (erro de sequência de função) na última chamada para **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obter mais informações sobre alterações comportamentais e como um aplicativo atua, consulte [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Aplicativos ODBC *2. x* e aplicativos ODBC *2. x* recompilados com os arquivos de cabeçalho ODBC *3. x* não chamam **SQLSetEnvAttr**. No entanto, eles chamam **SQLAllocEnv** em vez de **SQLAllocHandle** para alocar um identificador de ambiente. Portanto, quando o aplicativo chama **SQLAllocEnv** no Gerenciador de driver, o Gerenciador de driver chama **SQLAllocHandle** e **SQLSetEnvAttr** no driver. Assim, os drivers ODBC *3. x* sempre podem contar com esse atributo sendo definido.  
  
 Se um aplicativo compatível com padrões compilado com o sinalizador de compilação ODBC_STD chamar **SQLAllocEnv** (o que pode ocorrer porque **SQLAllocEnv** não é preterido em ISO), a chamada será mapeada para **SQLAllocHandleStd** no momento da compilação. Em tempo de execução, o aplicativo chama **SQLAllocHandleStd**. O Gerenciador de driver define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** é equivalente a uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3.  
  
 Em determinadas arquiteturas de driver, há a necessidade de o driver aparecer como um driver ODBC *2. x* ou um driver ODBC *3. x* , dependendo da conexão. O driver, nesse caso, pode não ser realmente um driver, mas uma camada que reside entre o Gerenciador de driver e outro driver. Por exemplo, ele pode imitar um driver, como o ODBC Spy. Em outro exemplo, ele pode atuar como um gateway, como EDA/SQL. Para aparecer como um driver ODBC *3. x* , esse driver deve ser capaz de exportar **SQLAllocHandle**e aparecer como um driver ODBC *2. x* , deve ser capaz de exportar **SQLAllocConnect**, **SQLAllocEnv**e **SQLAllocStmt**. Quando um ambiente, uma conexão ou uma instrução é alocada, o Gerenciador de driver verifica se esse driver exporta **SQLAllocHandle**. Como o driver faz, o Gerenciador de driver chama **SQLAllocHandle** no driver. Se o driver estiver trabalhando com um driver ODBC *2. x* , o driver deverá mapear a chamada **para SQLAllocHandle** para **SQLAllocConnect**, **SQLAllocEnv**ou **SQLAllocStmt**, conforme apropriado. Ele também deve fazer nada com a chamada **SQLSetEnvAttr** ao se comportar como um driver ODBC *2. x* .  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Tipo de dados datetime](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidade com versões anteriores de tipos de dados do C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Indicadores de comprimento fixo](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Suporte SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Retornar SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Chamar SQLSetPos para inserir dados](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Carregamento por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
