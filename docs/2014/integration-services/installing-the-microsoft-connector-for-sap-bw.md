---
title: Instalando o conector da Microsoft para 1,1 SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1a4362773ab6e0ec0252062d1695a921e7054226
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424743"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Instalando o Microsoft Connector para 1.1 SAP BW
  Para instalar o [!INCLUDE[msCoName](../includes/msconame-md.md)] conector 1,1 para SAP BW e sua documentação, baixe e execute o pacote do Windows Installer na página da Web do SQL Server Feature Pack.  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
## <a name="required-sap-files"></a>Arquivos necessários do SAP  
 Para usar o [!INCLUDE[msCoName](../includes/msconame-md.md)] conector 1,1 para SAP BW, não é necessário instalar o software de front-end do SAP (SAP GUI) no computador local.  
  
 No entanto, você deve copiar o arquivo do connector do SAP .NET, librfc32.dll, na subpasta do sistema na pasta Windows. (Normalmente, o local da pasta é **C:\Windows\system32**.)  
  
## <a name="considerations-for-64-bit-computers"></a>Considerações para computadores de 64 bits  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] conector 1,1 para SAP BW dá suporte total à versão de 64 bits do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Em um computador de 64 bits, o [!INCLUDE[msCoName](../includes/msconame-md.md)] conector 1,1 para SAP BW tem os seguintes requisitos adicionais:  
  
-   Para executar pacotes no modo de 64 bits em qualquer sistema operacional Windows de 64 bits, copie a versão de 64 bits do arquivo do SAP GUI, librfc32.dll, para a pasta **system32** da pasta Windows. (Normalmente, o local do arquivo é **C:\Windows\system32**.)  
  
-   Para executar pacotes no modo de 32 bits em qualquer sistema operacional Windows de 64 bits, copie o arquivo do SAP GUI, librfc32.dll, para a pasta **SysWow64** da pasta Windows. (Normalmente, o local da pasta é **C:\Windows\SysWow64**.)  
  
  
