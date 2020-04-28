---
title: Requisitos de hardware e software (ODBC) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295236"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware e de software (ODBC)
Este tópico lista os requisitos para usar os drivers de banco de dados da área de trabalho ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar os drivers de banco de dados da área de trabalho ODBC, você deve ter:  
  
-   Um computador pessoal compatível com IBM.  
  
-   Um disco rígido com 6 MB de espaço livre em disco.  
  
-   Pelo menos 16 MB de RAM (memória de acesso aleatório).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para acessar dados com um driver ODBC, você deve ter:  
  
-   O driver ODBC.  
  
-   O Gerenciador de driver ODBC de 32 bits, versão 3,51 ou posterior (Odbc32. dll).  
  
-   Microsoft Windows 95 ou posterior, ou Windows NT 4,0 ou Windows 2000.  
  
-   Um tamanho de pilha de pelo menos 20 KB para um aplicativo usando um driver ODBC da Microsoft.  
  
 Ao usar o Microsoft Windows NT 4,0 ou o Windows 2000, o driver de bits de 32 é thread-safe, mas apenas por meio do uso de um semáforo global que controla o acesso ao driver. O uso simultâneo do driver é muito limitado no Windows NT. Todo o acesso à camada Jet ISAM será de thread único para todos os aplicativos que usam o mecanismo do Microsoft Jet.  
  
 Ao executar vários aplicativos de 16 bits no Windows no Windows (WOW) no Microsoft Windows NT 4,0, os aplicativos devem ser executados em espaços de memória separados. (O mesmo espaço de memória não pode ser usado porque o ODBC não dá suporte a vários ambientes no mesmo processo.) Para executar um aplicativo em um espaço de memória separado, selecione o ícone do aplicativo no Gerenciador de programas, abra o menu **arquivo** e clique em **Propriedades**e, em seguida, clique em **executar em espaço de memória separado**.  
  
 Não há suporte para o uso desses drivers em aplicativos de 16 bits no Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de hardware e software específicos do driver  
  
-   O MicrosoftAccess e o dBASEdrivers podem exigir alterações nos arquivos Autoexec. bat ou config. sys.
