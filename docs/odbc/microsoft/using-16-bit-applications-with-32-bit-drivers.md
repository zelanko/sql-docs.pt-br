---
title: Uso de aplicativos de 16 bits com Drivers de 32 bits | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95ff3ce88daf4a508145c28ea194a97b9cbbbabe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso de aplicativos de 16 bits com Drivers de 32 bits
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Use o Gerenciador de driver de 32 bits ou 64 bits.  
  
 Você pode executar aplicativos de 16 bits com drivers de 32 bits em seu sistema baseado em Windows, desde que o driver de 32 bits não chamar funções de API do Win32 que criam threads explicitamente. O subsistema Windows on Windows (WOW) executa os aplicativos no modo de 16 bits e resolve chamadas de 16 bits para o sistema operacional. ODBC conversão chamadas de 16 bits de resolução de DLLs do aplicativo para drivers de 32 bits. Os aplicativos de 16 bits usam a API do Windows e os drivers de 32 bits usam a API do Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra como 16-bit aplicativos se comunicam com drivers de 32 bits. Entre o Gerenciador de Driver de 16 bits e os drivers de 32 bits são genéricos conversão DLLs que converte chamadas ODBC de 16 bits para chamadas ODBC de 32 bits.  
  
 ![Como 16 &#45; aplicativos de bits se comunicam com 32 &#45; bit drivers](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Sempre que um aplicativo de 16 bits interage com um driver de 32 bits, o Gerenciador de Driver de 32 bits sempre retorna "2.0" como a versão do ODBC com suporte pelo driver.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o administrador ODBC em computadores que executam o Microsoft® Windows® 2000, abra o painel de controle do Windows, clique duas vezes em **ferramentas administrativas**e, em seguida, clique duas vezes em **fontes de dados (ODBC)**. Em computadores que executam versões anteriores do Microsoft Windows, o ícone é chamado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
 A ilustração a seguir mostra como um aplicativo de 16 bits chama uma DLL de instalação do driver de 32 bits. Entre o DLL do instalador de 16 bits e o driver de 32 bits a DLL de configuração é uma DLL de conversão genérica que converte chamadas DLL do instalador de 16 bits para chamadas DLL do instalador de 32 bits.  
  
 ![Como um 16 &#45; bit aplicativo chama um 32 &#45; bit DLL de instalação do driver](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 No Windows on Windows (conversão de 16 bits para 32 bits), uma DLL de conversão adicional denominada Ds32gt.dll converte valores de argumento de 16 bits passados por meio de uma instalação de 32 bits DLL de volta para 16 bits.  
  
## <a name="components"></a>Componentes  
 O componente ODBC do MDAC 2.8 SP1 SDK inclui os seguintes arquivos para executar aplicativos de 16 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL de conversão genérico 16-bit ODBC|  
|Odbc32gt.dll|DLL de conversão genérico da ODBC de 32 bits|  
|ODBCCP32. dll|DLL de instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de 32 bits|  
|Odbcinst.hlp|Arquivo de Ajuda do instalador|  
|Ds16gt.dll|instalação de driver de 16 bits genérica de DLL de conversão|  
|CTL3D32|biblioteca de estilos de janela tridimensionais de 32 bits|  
  
 Além disso, os seguintes arquivos junto com o Gerenciador de Driver ODBC para 2.10 16 bits, que não fazem parte do ODBC 3.51, são necessários e devem ser instalados com o aplicativo de 16 bits.  
  
|Nome do arquivo|Description|  
|---------------|-----------------|  
|ODBC|Gerenciador de Driver de 16 bits|  
|Odbcinst|Instalador de 16 bits DLL|  
|Odbcadm.exe|programa de administrador ODBC de 16 bits|
