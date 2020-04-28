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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307597"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Usar aplicativos de 32 bits com drivers de 32 bits
Você pode executar aplicativos de 32 bits com drivers de 32 bits. Os aplicativos de 32 bits e os drivers de 32 bits usam a API de® do Win32.  
  
## <a name="architecture"></a>Arquitetura  
 A ilustração a seguir mostra como os aplicativos de 32 bits se comunicam com drivers de 32 bits. O aplicativo chama o Gerenciador de driver de 32 bits, que, por sua vez, chama drivers de 32 bits.  
  
 ![Como os aplicativos de 32 bits&#45;se comunicam com drivers de 32&#45;bits](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Não use a DLL do instalador de conversão de 32 bits no uam/Windows2000. Embora tenha o mesmo nome de arquivo que a DLL do instalador de 32 bits, ele é uma DLL diferente.  
  
## <a name="administration"></a>Administração  
 Você pode gerenciar fontes de dados para drivers de 32 bits usando o administrador de fonte de dados ODBC. Para abrir o Administrador ODBC em computadores que executam o Windows 2000, abra o painel de controle do Windows, clique duas vezes em **Ferramentas administrativas**e em **fontes de dados (ODBC)**. Em computadores que executam versões anteriores do Microsoft Windows, o ícone é denominado **ODBC de 32 bits** ou simplesmente **ODBC**.  
  
## <a name="components"></a>Componentes  
 O componente ODBC inclui os seguintes arquivos para executar aplicativos de 32 bits com drivers de 32 bits. Esses componentes estão no diretório \Redist.  
  
|Nome do arquivo|Descrição|  
|---------------|-----------------|  
|Odbc32. dll|Gerenciador de driver de 32 bits|  
|Odbccp32. dll|DLL do instalador de 32 bits|  
|Odbcad32. exe|programa de Administrador ODBC de 32 bits|  
|Odbcinst. hlp|Arquivo de ajuda do instalador|  
|Msvcrt40. dll|Biblioteca de tempo de execução C|
