---
title: Instalando o SMO | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 26438c3a9baea978aace0fc1383349f813e6c0d0
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
#<a name="installing-smo"></a>Instalando o SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Esta página fornece informações sobre como instalar o SMO para uso por aplicativos e os requisitos de sistema para usar o SMO.

## <a name="smo-nuget-package"></a>Pacote do NuGet SMO

Começando com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO é distribuído como o [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) pacote NuGet para permitir que os usuários a desenvolver aplicativos com o SMO.

Isso é uma substituição para SharedManagementObjects.msi, que foi lançada anteriormente como parte do Feature Pack SQL para cada versão do SQL Server. Aplicativos que usam o SMO devem ser atualizados para usar o pacote do NuGet em vez disso e serão responsáveis por garantir que os binários são instalados com o aplicativo que está sendo desenvolvido.

>>[!Important]
>>Conforme mencionado no [arquivos e números de versão](files-and-version-numbers.md) página, você não deve instalar os assemblies SMO no GAC. Isso pode causar problemas com outros aplicativos que também usam essas versões do SMO (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

##<a name="installing-the-package"></a>Instalando o pacote

Consulte [NuGet Quick Start - Use um pacote](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package) para obter instruções e exemplos de como instalar e usar um pacote do NuGet. 
  
## <a name="system-requirements"></a>Requisitos do sistema
  
 O SMO requer [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 em execução, para que os aplicativos usando devem garantir que computadores cliente têm essa versão ou superior instalado.
  
