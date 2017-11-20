---
title: Uso de aplicativos de 32 bits com Drivers de 32 bits | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e37da481e8068edb966b8f8ace4f129989cce990
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de aplicativos de 32 bits com Drivers de 32 bits
Você pode executar aplicativos de 32 bits com drivers de 32 bits. Os aplicativos de 32 bits e os drivers de 32 bits usam a API do Win32®.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra os aplicativos de 32 bits como se comunicam com drivers de 32 bits. O aplicativo chama o Gerenciador de Driver de 32 bits, que por sua vez, chama os drivers de 32 bits.  
  
 ![Como 32 &#45; aplicativos de bits se comunicam com 32 &#45; bit drivers](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
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

