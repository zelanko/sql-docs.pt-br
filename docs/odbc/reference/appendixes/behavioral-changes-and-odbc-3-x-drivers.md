---
title: Mudanças comportamentais e Drivers ODBC 3.x | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292360"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Alterações de comportamento e os drivers ODBC 3.x
O atributo de ambiente SQL_ATTR_ODBC_VERSION indica ao driver se ele precisa exibir comportamento ODBC *2.x* ou comportamento ODBC *3.x.* A forma como o SQL_ATTR_ODBC_VERSION atributo do ambiente é definido depende da aplicação. Os aplicativos ODBC *3.x* devem ligar para **o SQLSetEnvAttr** para definir esse atributo depois que eles chamarem **sqlAllocHandle** para alocar um cabo de ambiente e antes de chamar **o SQLAllocHandle** para alocar uma alça de conexão. Se eles não fizerem isso, o Driver Manager retorna SQLSTATE HY010 (erro de seqüência de funções) na última chamada para **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obter mais informações sobre mudanças comportamentais e como um aplicativo age, consulte [Mudanças comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Os aplicativos ODBC *2.x* e ODBC *2.x* recompilados com os arquivos de cabeçalho ODBC *3.x* não chamam **sqlsetenvAttr**. No entanto, eles chamam **SQLAllocEnv** em vez de **SQLAllocHandle** para alocar uma alça de ambiente. Portanto, quando o aplicativo chama **SQLAllocEnv** no Driver Manager, o Driver Manager chama **SQLAllocHandle** e **SQLSetEnvAttr** no driver. Assim, os drivers ODBC *3.x* sempre podem contar com este atributo sendo definido.  
  
 Se um aplicativo compatível com padrões compilado com o ODBC_STD compilar chamadas de bandeira **SQLAllocEnv** (o que pode ocorrer porque **o SQLAllocEnv** não é preterido no ISO), a chamada é mapeada para **SQLAllocHandleStd** no momento da compilação. No tempo de execução, o aplicativo chama **SQLAllocHandleStd**. O Driver Manager define o SQL_ATTR_ODBC_VERSION atributo de ambiente para SQL_OV_ODBC3. Uma chamada para **SQLAllocHandleStd** equivale a uma chamada para **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e uma chamada para **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3.  
  
 Em certas arquiteturas de driver, há a necessidade de o motorista aparecer como um driver ODBC *2.x* ou um driver ODBC *3.x,* dependendo da conexão. O motorista, neste caso, pode não ser realmente um motorista, mas uma camada que reside entre o Driver Manager e outro motorista. Por exemplo, ele pode imitar um driver, como o ODBC Spy. Em outro exemplo, ele pode atuar como um gateway, como o EDA/SQL. Para aparecer como um driver ODBC *3.x,* tal driver deve ser capaz de exportar **SQLAllocHandle**, e para aparecer como um driver ODBC *2.x,* deve ser capaz de exportar **SQLAllocConnect,** **SQLAllocEnv**e **SQLAllocStmt**. Quando um ambiente, conexão ou declaração deve ser alocado, o Driver Manager verifica se esse driver exporta **SQLAllocHandle**. Uma vez que o motorista faz, o Driver Manager chama **SQLAllocHandle** no driver. Se o driver estiver trabalhando com um driver ODBC *2.x,* o driver deverá mapear a chamada para **SQLAllocHandle** para **SQLAllocConnect,** **SQLAllocEnv**ou **SQLAllocStmt,** conforme apropriado. Ele também não deve fazer nada com a chamada **SQLSetEnvAttr** ao se comportar como um driver ODBC *2.x.*  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipo de dados datetime](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidade com versões anteriores de tipos de dados do C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Indicadores de comprimento fixo](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Suporte SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Retornando SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Chamando SQLSetPos para inserir dados](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Carregamento por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
