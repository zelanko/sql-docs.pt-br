---
title: Requisitos de hardware e Software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 389492c377105614c60c127041354786cabbd5ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware e Software (ODBC)
Este tópico lista os requisitos para usar os Drivers de banco de dados de área de trabalho do ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar os Drivers de banco de dados de área de trabalho do ODBC, você deve ter:  
  
-   Um PC compatíveis com IBM.  
  
-   Um disco rígido com 6 MB de espaço livre em disco.  
  
-   Pelo menos 16 MB de memória (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para acessar os dados com um driver ODBC, você deve ter:  
  
-   O driver ODBC.  
  
-   32 bits Gerenciador de Driver ODBC, versão 3.51 ou posterior (Odbc32. dll).  
  
-   Microsoft Windows 95 ou posterior, ou Windows NT 4.0 ou Windows 2000.  
  
-   Um tamanho de pilha de pelo menos 20 KB para um aplicativo usando um driver ODBC da Microsoft.  
  
 Ao usar o Microsoft Windows NT 4.0 ou Windows 2000, o driver de 32 bits é thread-safe, mas apenas com o uso de um semáforo global que controla o acesso para o driver. Uso simultâneo de driver é bastante limitado no Windows NT. Todo o acesso à camada de Jet ISAM será single-threaded para todos os aplicativos que usam o mecanismo do Microsoft Jet.  
  
 Quando a execução de vários aplicativos de 16 bits no Windows on Windows (WOW) no Microsoft Windows NT 4.0, os aplicativos devem ser executados em espaços de memória separados. (O mesmo espaço de memória não pode ser usado porque ODBC não dá suporte a vários ambientes no mesmo processo.) Para executar um aplicativo em um espaço de memória separado, selecione o ícone do aplicativo no Gerenciador do programa, abra o **arquivo** menu e clique em **propriedades**e, em seguida, clique em **executados na memória separado Espaço**.  
  
 Não há suporte para o uso desses drivers por aplicativos de 16 bits no Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de Software e Hardware específicos de driver  
  
-   O MicrosoftAccess e dBASEdrivers podem exigir alterações nos arquivos de arquivos Autoexec.bat ou sys.
