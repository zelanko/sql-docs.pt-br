---
title: Uso de aplicativos de 32 bits com Drivers de 32 bits | Microsoft Docs
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
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a07dae46125ce9ea04bfc36156d8855192396f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906431"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de aplicativos de 32 bits com Drivers de 32 bits
Você pode executar aplicativos de 32 bits com drivers de 32 bits. Os aplicativos de 32 bits e os drivers de 32 bits usam a API do Win32®.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra os aplicativos de 32 bits como se comunicam com drivers de 32 bits. O aplicativo chama o Gerenciador de Driver de 32 bits, que por sua vez, chama os drivers de 32 bits.  
  
 ![Como 32&#45;aplicativos de bits se comunicam com 32&#45;bit drivers](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Não use o instalador de conversão de 32 bits DLL no Windows NT/Windows 2000. Embora ele tenha o mesmo nome de arquivo que o DLL do instalador de 32 bits, é uma DLL diferente.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o administrador ODBC em computadores que executam o Windows 2000, abra o painel de controle do Windows, clique duas vezes em **ferramentas administrativas**e, em seguida, clique duas vezes em **fontes de dados (ODBC)**. Em computadores que executam versões anteriores do Microsoft Windows, o ícone é chamado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
## <a name="components"></a>Componentes  
 O componente ODBC inclui os seguintes arquivos para executar aplicativos de 32 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Description|  
|---------------|-----------------|  
|Odbc32.dll|Gerenciador de Driver de 32 bits|  
|ODBCCP32. dll|DLL de instalador de 32 bits|  
|Odbcad32.exe|programa de administrador ODBC de 32 bits|  
|Odbcinst.hlp|Arquivo de Ajuda do instalador|  
|Msvcrt40.|Biblioteca de tempo de execução do C|
