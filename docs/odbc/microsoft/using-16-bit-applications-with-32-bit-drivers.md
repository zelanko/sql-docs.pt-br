---
title: Usando aplicativos de 16 bits com drivers de 32 bits | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307627"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 16 bits com drivers de 32 bits
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. Use o gerenciador de driver de 32 ou 64 bits em vez disso.  
  
 Você pode executar aplicativos de 16 bits com drivers de 32 bits no sistema baseado no Windows, desde que o driver de 32 bits não chame explicitamente as funções de API do Win32 que criam threads. O subsistema Windows on Windows (WOW) executa os aplicativos no modo de 16 bits e resolve chamadas de 16 bits para o sistema operacional. Os DLLs de thunking oDBC resolvem chamadas de 16 bits do aplicativo para drivers de 32 bits. Os aplicativos de 16 bits usam a API do Windows e os drivers de 32 bits usam a API Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra como aplicativos de 16 bits se comunicam com drivers de 32 bits. Entre o Driver Manager de 16 bits e os drivers de 32 bits estão DLLs genéricos que convertem chamadas ODBC de 16 bits para chamadas ODBC de 32 bits.  
  
 ![Como aplicativos de bits de 16&#45;se comunicam com drivers de bits de 32&#45;](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Sempre que um aplicativo de 16 bits interage com um driver de 32 bits, o Driver Manager de 32 bits sempre retorna "2.0" como a versão do ODBC suportada pelo driver.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o Administrador de Origem de Dados oDBC. Para abrir o administrador ODBC em computadores que executam o Microsoft® O Windows® 2000, abra o Painel de Controle do Windows, clique duas vezes em **Ferramentas Administrativas**e clique duas vezes em Fontes de **Dados (ODBC).** Em computadores que executam versões anteriores do Microsoft Windows, o ícone é chamado **de ODBC de 32 bits** ou simplesmente **ODBC**.  
  
 A ilustração a seguir mostra como um aplicativo de 16 bits chama um DLL de configuração de driver de 32 bits. Entre o instalador de 16 bits DLL e a configuração de driver de 32 bits, o DLL é um DLL genérico que converte chamadas DLL do instalador de 16 bits para chamadas DLL instaladoras de 32 bits.  
  
 ![Como um aplicativo de bits de 16&#45;chama um Driver de 32&#45;configuração de driver de bits DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 No Windows on Windows (thunking de 16 bits a 32 bits), um DLL adicional chamado Ds32gt.dll converte valores de argumento de 16 bits passados através de uma configuração dll de 32 bits de volta para 16 bits.  
  
## <a name="components"></a>Componentes  
 O componente ODBC do MDAC 2.8 SP1 SDK inclui os seguintes arquivos para executar aplicativos de 16 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL genérico ODBC de 16 bits|  
|Odbc32gt.dll|DLL genérico ODBC de 32 bits|  
|Odbccp32.dll|Instalador de 32 bits DLL|  
|Odbcad32.exe|Programa de administrador de 32 bits|  
|Odbcinst.hlp|Arquivo de ajuda do instalador|  
|Ds16gt.dll|Configuração do driver de 16 bits genérico thunking DLL|  
|Ctl3d32.dll|Biblioteca de estilo de janela tridimensional de 32 bits|  
  
 Além disso, os seguintes arquivos, juntamente com o Gerenciador de Driver ODBC 2.10 de 16 bits, que não fazem parte do ODBC 3.51, são exigidos e devem ser instalados com o aplicativo de 16 bits.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc.dll|Gerenciador de driver de 16 bits|  
|Odbcinst.dll|DLL instalador de 16 bits|  
|Odbcadm.exe|Programa de administrador ODBC de 16 bits|
