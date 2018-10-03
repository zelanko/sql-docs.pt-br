---
title: Usando aplicativos de 16 bits com Drivers de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752924"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 16 bits com drivers de 32 bits
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. Use o Gerenciador de driver de 32 bits ou 64 bits.  
  
 Você pode executar aplicativos de 16 bits com drivers de 32 bits em seu sistema baseado em Windows, desde que o driver de 32 bits não chama explicitamente funções de API do Win32 que criam threads. O Windows no subsistema do Windows (WOW) executa os aplicativos no modo de 16 bits e resolve chamadas de 16 bits para o sistema operacional. ODBC conversão DLLs resolver chamadas de 16 bits do aplicativo para drivers de 32 bits. Os aplicativos de 16 bits usam a API do Windows e os drivers de 32 bits usam a API do Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra os aplicativos como de 16 bits se comunicam com drivers de 32 bits. Entre o Gerenciador de Driver de 16 bits e os drivers de 32 bits são genéricos conversão DLLs que convertem chamadas ODBC de 16 bits para chamadas ODBC de 32 bits.  
  
 ![Como 16&#45;aplicativos de bits se comunicam com 32&#45;bit drivers](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Sempre que um aplicativo de 16 bits interage com um driver de 32 bits, o Gerenciador de Driver de 32 bits sempre retorna "2.0" como a versão do ODBC com suporte pelo driver.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o administrador ODBC em computadores que executam o Microsoft® Windows® 2000, abra o painel de controle do Windows, clique duas vezes **ferramentas administrativas**e, em seguida, clique duas vezes em **fontes de dados (ODBC)**. Em computadores que executam versões anteriores do Microsoft Windows, o ícone é denominado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
 A ilustração a seguir mostra como um aplicativo de 16 bits chama uma DLL de instalação do driver de 32 bits. Entre a DLL do instalador de 16 bits e o driver de 32 bits a DLL de instalação é uma DLL de conversão genérica que converte as chamadas DLL do instalador de 16 bits para chamadas de DLL do instalador de 32 bits.  
  
 ![Como um 16&#45;aplicativo de bit chama um 32&#45;bit DLL de instalação do driver](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 No Windows no Windows (conversão de 16 bits para 32 bits), uma DLL de conversão adicional denominada converte Ds32gt.dll valores de argumento de 16 bits passados por meio de uma instalação de 32 bits DLL de volta para 16 bits.  
  
## <a name="components"></a>Componentes  
 O componente ODBC do SDK MDAC 2.8 SP1 inclui os seguintes arquivos para a execução de aplicativos de 16 bits com drivers de 32 bits. Esses componentes estão na pasta \Redist.  
  
|Nome do arquivo|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL de conversão genérico de ODBC 16 bits|  
|Odbc32gt.dll|DLL de conversão genérico de ODBC 32-bit|  
|Odbccp32.dll|DLL do instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de 32 bits|  
|Odbcinst.hlp|Arquivo de Ajuda do instalador|  
|Ds16gt.dll|instalação do driver de 16 bits genérica de DLL de conversão|  
|CTL3D32|biblioteca de estilos de janela tridimensionais de 32 bits|  
  
 Além disso, os seguintes arquivos, juntamente com o Gerenciador de Driver ODBC para 2.10 16 bits, que não fazem parte do ODBC 3.51, são exigidos pelo e devem ser instalados com o aplicativo de 16 bits.  
  
|Nome do arquivo|Description|  
|---------------|-----------------|  
|ODBC|Gerenciador de Driver de 16 bits|  
|Odbcinst|DLL do instalador de 16 bits|  
|Odbcadm.exe|programa de administrador de ODBC de 16 bits|
