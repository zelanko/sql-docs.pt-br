---
title: Componentes
description: Saiba mais sobre os componentes do SQL Server Native Client como sqlncli11.dll, sqlnclir11. rll, sqlncli. h e sqlncli11. lib.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f298c7e3c453da1a20826d91509ca61778ad65b0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965167"
---
# <a name="components-of-sql-server-native-client"></a>Componentes do SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contém os seguintes componentes:  
  
|Componente|Descrição|  
|---------------|-----------------|  
|sqlncli11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Isso inclui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|O arquivo de recursos que acompanha a biblioteca do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|O arquivo do cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contém todas as novas definições necessárias para usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esse arquivo de cabeçalho substitui os arquivos de cabeçalho odbcss.h e sqloledb.h.<br /><br /> Observação: não é possível referenciar sqlncli. h e odbcss. h no mesmo programa, mas você pode fazer referência a sqlncli. h e SQLOLEDB. h no mesmo programa, contanto que SQLOLEDB. h seja definido primeiro.|  
|sqlncli11.lib|O arquivo de biblioteca necessário para chamar diretamente as funções do utilitário **bcp** que fazem parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client.<br /><br /> Observação: se você referenciar o arquivo sqlncli11. lib em seu código de programação, precisará certificar-se de que o arquivo de sqlncli11.dll está no caminho do sistema e no caminho do sistema dos usuários que fazem uso do seu aplicativo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
