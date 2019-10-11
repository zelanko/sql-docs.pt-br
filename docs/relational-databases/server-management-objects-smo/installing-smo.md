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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cabd2d1ebbe726971e7837ff3e268ad3c2cee89f
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041264"
---
# <a name="installing-smo"></a>Instalando o SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Esta página fornece informações sobre como instalar o SMO para uso por aplicativos e os requisitos de sistema para usar o SMO.

## <a name="smo-nuget-package"></a>Pacote NuGet do SMO

A partir do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 Smo é distribuído como o pacote NuGet [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) para permitir que os usuários desenvolvam aplicativos como Smo.

Essa é uma substituição para o SharedManagementObjects. msi, que foi lançado anteriormente como parte do SQL Feature Pack para cada versão do SQL Server. Os aplicativos que usam o SMO devem ser atualizados para usar o pacote NuGet e serão responsáveis por garantir que os binários sejam instalados com o aplicativo que está sendo desenvolvido.

>>[!Important]
>>Conforme mencionado na página [arquivos e números de versão](files-and-version-numbers.md) , você não deve instalar os assemblies SMO no GAC. Isso pode causar problemas com outros aplicativos que também usam essas versões do SMO (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

## <a name="installing-the-package"></a>Instalando o pacote

Consulte [NuGet início rápido-use um pacote](https://docs.microsoft.com/nuget/quickstart/use-a-package) para obter instruções e exemplos de instalação e uso de um pacote NuGet. 
  
## <a name="system-requirements"></a>Requisitos de sistema
  
 O SMO requer que [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4,0 ou o .NET Core 2,0 seja executado, portanto, todos os aplicativos que o utilizam devem garantir que os computadores cliente tenham essa versão ou superior instalada. Alguns binários nativos instalados com as bibliotecas NetFx SMO também exigem que o tempo de execução do VC 2013 seja instalado; esse tempo de execução não está incluído no pacote. Você pode baixar o Redist apropriado para sua arquitetura de destino do https://www.microsoft.com/download/details.aspx?id=40784
  
