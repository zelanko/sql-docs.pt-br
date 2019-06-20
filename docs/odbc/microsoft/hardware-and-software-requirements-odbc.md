---
title: Requisitos de hardware e Software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f40621645aad2d1e52cb0a89baa8ff29b01446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471317"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware e de software (ODBC)
Este tópico lista os requisitos para usar os Drivers de banco de dados de área de trabalho do ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar os Drivers de banco de dados de área de trabalho do ODBC, você deve ter:  
  
-   Um computador pessoal de compatível com o IBM.  
  
-   Um disco rígido com 6 MB de espaço livre em disco.  
  
-   Pelo menos 16 MB de memória (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para acessar dados com um driver ODBC, você deve ter:  
  
-   O driver ODBC.  
  
-   Os 32 bits Gerenciador de Driver ODBC versão 3.51 ou posterior (Odbc32. dll).  
  
-   Microsoft Windows 95 ou posterior, ou Windows NT 4.0 ou Windows 2000.  
  
-   Um tamanho de pilha de pelo menos 20 KB para um aplicativo usando um driver ODBC do Microsoft.  
  
 Ao usar o Microsoft Windows NT 4.0 ou Windows 2000, o driver de 32 bits é thread-safe, mas apenas com o uso de um semáforo global que controla o acesso ao driver. Uso simultâneo do driver é bastante limitado no Windows NT. Todo o acesso à camada de Jet ISAM será single-threaded para todos os aplicativos que usam o mecanismo Microsoft Jet.  
  
 Ao executar vários aplicativos de 16 bits no Windows on Windows (WOW) no Microsoft Windows NT 4.0, os aplicativos devem ser executados em espaços de memória separados. (O mesmo espaço de memória não pode ser usado porque ODBC não oferece suporte a vários ambientes no mesmo processo.) Para executar um aplicativo em um espaço de memória separada, selecione o ícone do aplicativo no Gerenciador de programa, abra o **arquivo** menu e clique em **propriedades**e, em seguida, clique em **executados na memória separada Espaço**.  
  
 Não há suporte para o uso desses drivers por aplicativos de 16 bits no Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos específicos de driver de Hardware e Software  
  
-   O MicrosoftAccess e dBASEdrivers podem exigir alterações nos arquivos Autoexec. bat ou config. sys.
