---
title: Instalar e desinstalar o componente de origem OData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86aa25f148c44343a57e0e55831663155d288830
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374438"
---
# <a name="install-and-uninstall-odata-source-component"></a>Instalar e desinstalar o componente de origem do OData
  Este tópico fornece instruções para instalar ou remover o componente de origem OData em seu computador.  
  
## <a name="installation"></a>Instalação  
 O componente de origem OData exige que os seguintes componentes sejam instalados em seu computador.  
  
-   Ferramentas de dados do SQL Server (para criar pacotes)  
  
-   SQL Server Integration Services (para executar pacotes fora do Visual Studio)  
  
 Para instalar o componente de origem OData, baixe o [SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkId=391999) e execute um dos arquivos MSI a seguir.  
  
-   ODataSourceForSQLServer2014-amd64.msi para plataformas 64 bits  
  
-   ODataSourceForSQLServer2014-x86.msi para plataformas 32 bits  
  
> [!IMPORTANT]  
>  O instalador de 64 bits instalará as versões de 32 bits e de 64 bits do componente de origem OData. Você só precisará executar o instalador de 32 bits se você estiver usando um sistema operacional de 32 bits.  
  
## <a name="uninstallation"></a>Desinstalação  
 O componente de origem OData pode ser desinstalado no menu **Programas e Recursos** . Encontrar a entrada **Componente de origem do Microsoft SQL Server SSIS OData (x64)** e clique em **Desinstalar**.  
  
  
