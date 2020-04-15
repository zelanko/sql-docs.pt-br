---
title: Usando aplicativos de 32 bits com drivers de 32 bits | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31512f9339b9d46225bb4f1198cb617a48509acb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307597"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 32 bits com drivers de 32 bits
Você pode executar aplicativos de 32 bits com drivers de 32 bits. Os aplicativos de 32 bits e os drivers de 32 bits usam a API ® Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra como aplicativos de 32 bits se comunicam com drivers de 32 bits. O aplicativo chama o Driver Manager de 32 bits, que por sua vez chama drivers de 32 bits.  
  
 ![Como aplicativos de bits de 32&#45;se comunicam com drivers de bits de 32&#45;](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Não use o instalador de 32 bits DLL no WindowsNT/Windows2000. Embora tenha o mesmo nome de arquivo do instalador de 32 bits DLL, é um DLL diferente.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o Administrador de Origem de Dados oDBC. Para abrir o Administrador ODBC em computadores que executam o Windows 2000, abra o Painel de Controle do Windows, clique duas vezes em **Ferramentas Administrativas**e clique duas vezes em Fontes de **Dados (ODBC).** Em computadores que executam versões anteriores do Microsoft Windows, o ícone é chamado **de ODBC de 32 bits** ou simplesmente **ODBC**.  
  
## <a name="components"></a>Componentes  
 O componente ODBC inclui os seguintes arquivos para executar aplicativos de 32 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc32.dll|Gerenciador de driver de 32 bits|  
|Odbccp32.dll|DLL instalador de 32 bits|  
|Odbcad32.exe|Programa de administrador ODBC de 32 bits|  
|Odbcinst.hlp|Arquivo de ajuda do instalador|  
|Msvcrt40.dll|Biblioteca c de tempo de execução|
