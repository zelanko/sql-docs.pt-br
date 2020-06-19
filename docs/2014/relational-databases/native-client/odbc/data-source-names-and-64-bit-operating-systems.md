---
title: Nomes de fontes de dados e sistemas operacionais de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: rothja
ms.author: jroth
ms.openlocfilehash: ae31584ca3c076919f688d1ef9bdef80706c6940
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055848"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nomes de fonte de dados e sistemas operacionais de 64 bits
  Para compilar e executar um aplicativo como sendo de 32 bits em um sistema operacional de 64 bits, você precisa criar a fonte de dados ODBC com o Administrador ODBC em %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Comentários  
 Um sistema operacional Windows de 64 bits tem dois arquivos odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe é usado criar e manter nomes da fonte de dados para aplicativos de 64 bits.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe é usado criar e manter nomes da fonte de dados para aplicativos de 32 bits, incluindo aplicativos de 32 bits que são executados em sistemas operacionais de 64 bits.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
