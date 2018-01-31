---
title: Instalar o Microsoft Connector para SAP BW | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1d2716714e810143e17d3435c61de394e82b9bc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="installing-the-microsoft-connector-for-sap-bw"></a>Instalação do Microsoft Connector para SAP BW
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW para SQL Server 2016 é um componente do SQL Server 2016 Feature Pack. Para instalar o Connector for SAP BW e sua documentação, baixe e execute o instalador na [página Web do SQL Server 2016 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=746297).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
## <a name="required-sap-files"></a>Arquivos necessários do SAP  
 Para usar o [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector para SAP BW, não é necessário instalar o SAP Front End software (SAP GUI) no computador local.  
  
 No entanto, você deve copiar o arquivo do connector do SAP .NET, librfc32.dll, na subpasta do sistema na pasta Windows. (Normalmente, o local da pasta é **C:\Windows\system32**.)  
  
## <a name="considerations-for-64-bit-computers"></a>Considerações para computadores de 64 bits  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector para SAP BW dá suporte total à versão de 64 bits do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Em um computador de 64 bits, o [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector para SAP BW tem os seguintes requisitos adicionais:  
  
-   Para executar pacotes no modo de 64 bits em qualquer sistema operacional Windows de 64 bits, copie a versão de 64 bits do arquivo do SAP GUI, librfc32.dll, para a pasta **system32** da pasta Windows. (Normalmente, o local do arquivo é **C:\Windows\system32**.)  
  
-   Para executar pacotes no modo de 32 bits em qualquer sistema operacional Windows de 64 bits, copie o arquivo do SAP GUI, librfc32.dll, para a pasta **SysWow64** da pasta Windows. (Normalmente, o local da pasta é **C:\Windows\SysWow64**.)  
  
  
