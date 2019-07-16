---
title: Excluir uma fonte de dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbd14b4f784f93f78c317268799571220da3a3c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939572"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>Configurar o Driver ODBC do SQL Server – Excluir uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Antes de usar os aplicativos ODBC com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, você deve saber como atualizar a versão dos procedimentos armazenados de catálogo em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar, excluir e testar as fontes de dados.  
  
  Você pode excluir uma fonte de dados usando o administrador de ODBC, programaticamente (usando [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), ou excluindo um arquivo (se um nome de fonte de dados de arquivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para excluir uma fonte de dados usando o Administrador de ODBC  
  
1.  Na **painel de controle**, abra **ferramentas administrativas**e, em seguida, clique duas vezes em qualquer um **fontes de dados ODBC (64 bits)** ou **fontes de dados ODBC (32 bits)** . Alternativamente, você pode executar odbcad32.exe no prompt de comando.  
  
2.  Clique o **DSN de usuário**, **DSN de sistema**, ou **DSN de arquivo** guia.  
  
3.  Selecione a fonte de dados para excluir.  
  
4.  Clique em **remover**e, em seguida, confirme a exclusão.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example"></a>Exemplo  
 Para excluir programaticamente uma fonte de dados, chame [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) usando ODBC_REMOVE_DSN ou ODBC_REMOVE_SYS_DSN como o segundo parâmetro.  
  
 O exemplo a seguir mostra como você pode excluir programaticamente uma fonte de dados.  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include \<windows.h>  
#include \<odbcinst.h>  
  
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
 [Adicionar uma fonte de dados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
