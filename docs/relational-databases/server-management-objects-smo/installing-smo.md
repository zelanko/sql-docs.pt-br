---
title: Instalando o SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 97c7159682e421005385fd830ceed4380086089c
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432259"
---
# <a name="installing-smo"></a>Instalando o SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Esta página fornece informações sobre como instalar o SMO para uso por aplicativos e os requisitos do sistema para usar o SMO.

## <a name="smo-nuget-package"></a>Pacote do NuGet SMO

Começando com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO é distribuído como o [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) pacote do NuGet para permitir que os usuários a desenvolver aplicativos com o SMO.

Isso é uma substituição para sharedmanagementobjects. msi, que foi lançada anteriormente como parte do Feature Pack SQL para cada versão do SQL Server. Aplicativos que usam o SMO devem ser atualizados para usar o pacote do NuGet em vez disso e serão responsáveis por garantir que os binários são instalados com o aplicativo que está sendo desenvolvido.

>>[!Important]
>>Como mencionado na [arquivos e números de versão](files-and-version-numbers.md) página, você não deve instalar os assemblies SMO no GAC. Isso poderia causar problemas com outros aplicativos que também usam essas versões do SMO (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

## <a name="installing-the-package"></a>A instalação do pacote

Ver [início rápido NuGet – Use um pacote](https://docs.microsoft.com/nuget/quickstart/use-a-package) para obter instruções e exemplos de como instalar e usar um pacote do NuGet. 
  
## <a name="system-requirements"></a>Requisitos do sistema
  
 Requer o SMO [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 em execução, portanto, quaisquer aplicativos que a utilizam devem garantir que os computadores cliente tem essa versão ou superior instalado. Alguns binários nativos instalados com as bibliotecas de SMO NetFx também exigem o tempo de execução do VC 2013 instalado; Esse tempo de execução não está incluído no pacote. Você pode baixar o apropriado para sua arquitetura de destino do pacote redistribuível https://www.microsoft.com/download/details.aspx?id=40784
  
