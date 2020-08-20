---
description: Usar aplicativos de 16 bits com drivers de 32 bits
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
ms.openlocfilehash: c54dc53e5a8e6d3322bfa74ec6904cebca434b8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471383"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 16 bits com drivers de 32 bits
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. Em vez disso, use o Gerenciador de drivers de 32 bits ou 64 bits.  
  
 Você pode executar aplicativos de 16 bits com drivers de 32 bits em seu sistema baseado em Windows, desde que o driver de bit 32 não chame explicitamente as funções de API do Win32 que criam threads. O subsistema Windows no Windows (WOW) executa os aplicativos no modo de 16 bits e resolve chamadas de 16 bits para o sistema operacional. As DLLs de conversão ODBC resolvem chamadas de 16 bits do aplicativo para drivers de 32 bits. Os aplicativos de 16 bits usam a API do Windows e os drivers de 32 bits usam a API do Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra como os aplicativos de 16 bits se comunicam com os drivers de 32 bits. Entre o Gerenciador de driver de 16 bits e os drivers de 32 bits estão as DLLs de conversão genérica que convertem chamadas ODBC de 16 bits para chamadas ODBC de 32 bits.  
  
 ![Como 16 aplicativos de&#45;bits se comunicam com drivers de 32&#45;bits](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  A qualquer momento que um aplicativo de 16 bits interage com um driver de 32 bits, o Gerenciador de driver de 32 bits sempre retorna "2,0" como a versão do ODBC suportada pelo driver.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o Administrador ODBC em computadores que executam o Microsoft® Windows® 2000, abra o painel de controle do Windows, clique duas vezes em **Ferramentas administrativas**e clique duas vezes em **fontes de dados (ODBC)**. Em computadores que executam versões anteriores do Microsoft Windows, o ícone é denominado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
 A ilustração a seguir mostra como um aplicativo de 16 bits chama uma DLL de instalação de driver de 32 bits. Entre a DLL do instalador de 16 bits e a DLL de instalação do driver de 32 bits é uma DLL de conversão genérica que converte chamadas de DLL de instalador de 16 bits para chamadas de DLL de instalador de 32 bits.  
  
 ![Como um aplicativo de 16&#45;bits chama uma DLL de instalação de driver de 32&#45;bits](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 No Windows no Windows (conversão de 16 bits para 32 bits), uma DLL de conversão adicional chamada Ds32gt.dll converte valores de argumento de 16 bits passados por uma DLL de instalação de 32 bits de volta para 16 bits.  
  
## <a name="components"></a>Componentes  
 O componente ODBC do SDK do MDAC 2,8 SP1 inclui os seguintes arquivos para executar aplicativos de 16 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL de conversão genérica ODBC de 16 bits|  
|Odbc32gt.dll|DLL de conversão genérica ODBC de 32 bits|  
|Odbccp32.dll|DLL do instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de 32 bits|  
|Odbcinst. hlp|Arquivo de ajuda do instalador|  
|Ds16gt.dll|DLL de conversão genérica de configuração de driver de 16 bits|  
|Ctl3d32.dll|biblioteca de estilos de janela tridimensional de 32 bits|  
  
 Além disso, os seguintes arquivos, juntamente com o Gerenciador de driver ODBC 2,10 de 16 bits, que não fazem parte do ODBC 3,51, são exigidos pelo e devem ser instalados com o aplicativo de 16 bits.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc.dll|Gerenciador de driver de 16 bits|  
|Odbcinst.dll|DLL de instalador de 16 bits|  
|Odbcadm.exe|programa de Administrador ODBC de 16 bits|
