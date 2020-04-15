---
title: Requisitos de Hardware e Software (ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295236"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware e de software (ODBC)
Este tópico lista os requisitos para usar os Drivers de banco de dados de desktop da ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar os drivers de banco de dados de desktop do ODBC, você deve ter:  
  
-   Um computador pessoal compatível com a IBM.  
  
-   Um disco rígido com 6 MB de espaço livre em disco.  
  
-   Pelo menos 16 MB de memória de acesso aleatório (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para acessar dados com um driver ODBC, você deve ter:  
  
-   O motorista da ODBC.  
  
-   O Gerenciador de Driver ODBC de 32 bits, versão 3.51 ou posterior (Odbc32.dll).  
  
-   Microsoft Windows 95 ou posterior, ou Windows NT 4.0 ou Windows 2000.  
  
-   Um tamanho de pilha de pelo menos 20 KB para um aplicativo usando um driver Microsoft ODBC.  
  
 Ao usar o Microsoft Windows NT 4.0 ou o Windows 2000, o driver de 32 bits é seguro para threads, mas apenas através do uso de um semáforo global que controla o acesso ao driver. O uso simultâneo do driver é muito limitado no Windows NT. Todo o acesso à camada Jet ISAM será de um único rosca para todos os aplicativos usando o motor Microsoft Jet.  
  
 Ao executar vários aplicativos de 16 bits no Windows on Windows (WOW) no Microsoft Windows NT 4.0, os aplicativos devem ser executados em espaços de memória separados. (O mesmo espaço de memória não pode ser usado porque o ODBC não suporta vários ambientes no mesmo processo.) Para executar um aplicativo em um espaço de memória separado, selecione o ícone do aplicativo no Gerenciador de programas, abra o menu **Arquivo** e clique **em Propriedades**e clique em Executar em espaço de **memória separado**.  
  
 O uso desses drivers por aplicativos de 16 bits no Windows 95 não é suportado.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos específicos de hardware e software específicos para o motorista  
  
-   Os microsoftaccess e dBASEdrivers podem exigir alterações nos arquivos Autoexec.bat ou Config.sys.
