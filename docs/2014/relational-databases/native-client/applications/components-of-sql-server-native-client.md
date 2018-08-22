---
title: Componentes do SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a586634854cbf2b18f44558fca4c0d283f8011f9
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392009"
---
# <a name="components-of-sql-server-native-client"></a>Componentes do SQL Server Native Client
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contém os seguintes componentes:  
  
|Componente|Description|  
|---------------|-----------------|  
|sqlncli11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Isso inclui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|O arquivo de recursos que acompanha a biblioteca do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|s10ch_sqlncli.chm|O arquivo de Ajuda do Assistente de Fonte de Dados que documenta como criar uma fonte de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ou o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlncli.h|O arquivo do cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contém todas as novas definições necessárias para usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esse arquivo de cabeçalho substitui os arquivos de cabeçalho odbcss.h e sqloledb.h. **Observação:** você não pode referenciar SQLNCLI. h e Odbcss. h no mesmo programa, mas você pode referenciar SQLNCLI. h e SQLOLEDB. h no mesmo programa, desde que SQLOLEDB. h é definida pela primeira vez.|  
|sqlncli11.lib|O arquivo de biblioteca necessário para chamar diretamente as **bcp** funções de utilitário que fazem parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. **Observação:** se você referenciar o arquivo sqlncli11.lib no código de programação, você precisa certificar-se de que o arquivo sqlncli11.dll está no caminho do sistema e no caminho do sistema dos usuários que fazem uso de seu aplicativo.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
