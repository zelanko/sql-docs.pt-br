---
title: Excluir uma fonte de dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d3b18bfe882147e0c60033dac9efd9dc4e3a6057
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009538"
---
# <a name="delete-a-data-source-odbc"></a>Excluir uma fonte de dados (ODBC)
  Você pode excluir uma fonte de dados usando o administrador de ODBC, programaticamente (usando [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)), ou excluindo um arquivo (se um nome de fonte de dados de arquivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para excluir uma fonte de dados usando o Administrador de ODBC  
  
1.  Em **painel de controle**, abra **ferramentas administrativas**e, em seguida, clique duas vezes em **fontes de dados (ODBC)**. Alternativamente, você pode executar odbcad32.exe no prompt de comando.  
  
2.  Clique o **DSN do usuário**, **DSN de sistema**, ou **DSN de arquivo** guia.  
  
3.  Clique na fonte de dados para excluir.  
  
4.  Clique em **remover**e, em seguida, confirme a exclusão.  
  
## <a name="example"></a>Exemplo  
 Para excluir programaticamente uma fonte de dados, chame [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) usando ODBC_REMOVE_DSN ou ODBC_REMOVE_SYS_DSN como o segundo parâmetro.  
  
 O exemplo a seguir mostra como você pode excluir programaticamente uma fonte de dados.  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include <windows.h>  
#include <odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instrução sobre a configuração do driver ODBC do SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  