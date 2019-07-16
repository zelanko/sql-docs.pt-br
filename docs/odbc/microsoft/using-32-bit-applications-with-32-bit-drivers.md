---
title: Usando aplicativos de 32 bits com Drivers de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b4d14cc65b31a0641149ace931efe46c914ad1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088162"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 32 bits com drivers de 32 bits
Você pode executar aplicativos de 32 bits com drivers de 32 bits. Os aplicativos de 32 bits e os drivers de 32 bits usam a API do Win32®.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra os aplicativos de 32 bits como se comunicam com drivers de 32 bits. O aplicativo chama o Gerenciador de Driver de 32 bits, que por sua vez chama os drivers de 32 bits.  
  
 ![Como 32&#45;aplicativos de bits se comunicam com 32&#45;bit drivers](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Não use a DLL do instalador conversão de 32 bits no Windows NT/Windows 2000. Embora ele tenha o mesmo nome de arquivo que o DLL do instalador de 32 bits, ele é uma DLL diferente.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o administrador ODBC em computadores que executam o Windows 2000, abra o painel de controle do Windows, clique duas vezes **ferramentas administrativas**e, em seguida, clique duas vezes em **fontes de dados (ODBC)** . Em computadores que executam versões anteriores do Microsoft Windows, o ícone é denominado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
## <a name="components"></a>Componentes  
 O componente ODBC inclui os seguintes arquivos para a execução de aplicativos de 32 bits com drivers de 32 bits. Esses componentes estão na pasta \Redist.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc32.dll|Gerenciador de Driver de 32 bits|  
|Odbccp32.dll|DLL do instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de ODBC de 32 bits|  
|Odbcinst.hlp|Arquivo de Ajuda do instalador|  
|Msvcrt40.dll|Biblioteca de tempo de execução do C|
