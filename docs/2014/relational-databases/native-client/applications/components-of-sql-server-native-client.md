---
title: Componentes de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 329ffa78471ead02b1431a41d898cfc43ca65684
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63213518"
---
# <a name="components-of-sql-server-native-client"></a>Componentes do SQL Server Native Client
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contém os seguintes componentes:  
  
|Componente|DESCRIÇÃO|  
|---------------|-----------------|  
|sqlncli11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Isso inclui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|O arquivo de recursos que acompanha a biblioteca do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|s10ch_sqlncli.chm|O arquivo de Ajuda do Assistente de Fonte de Dados que documenta como criar uma fonte de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ou o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlncli.h|O arquivo do cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contém todas as novas definições necessárias para usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esse arquivo de cabeçalho substitui os arquivos de cabeçalho odbcss.h e sqloledb.h. **Observação:**  Não é possível referenciar sqlncli. h e odbcss. h no mesmo programa, mas você pode fazer referência a sqlncli. h e SQLOLEDB. h no mesmo programa, contanto que SQLOLEDB. h seja definido primeiro.|  
|sqlncli11.lib|O arquivo de biblioteca necessário para chamar diretamente as funções do utilitário **bcp** que fazem parte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do driver ODBC do Native Client. **Observação:**  Se você fizer referência ao arquivo sqlncli11. lib no código de programação, precisará certificar-se de que o arquivo sqlncli11. dll esteja no caminho do sistema e no caminho do sistema dos usuários que usam seu aplicativo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
