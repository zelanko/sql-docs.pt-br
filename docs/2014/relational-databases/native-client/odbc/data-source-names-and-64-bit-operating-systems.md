---
title: Sistemas operacionais de 64 bits e de nomes de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb7d29b7196f4c1e43de06a0a8fc17dae5acec9c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431845"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nomes de fonte de dados e sistemas operacionais de 64 bits
  Para compilar e executar um aplicativo como sendo de 32 bits em um sistema operacional de 64 bits, você precisa criar a fonte de dados ODBC com o Administrador ODBC em %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Remarks  
 Um sistema operacional Windows de 64 bits tem dois arquivos odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe é usado criar e manter nomes da fonte de dados para aplicativos de 64 bits.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe é usado criar e manter nomes da fonte de dados para aplicativos de 32 bits, incluindo aplicativos de 32 bits que são executados em sistemas operacionais de 64 bits.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
