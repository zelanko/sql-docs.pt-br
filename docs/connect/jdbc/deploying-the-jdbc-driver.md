---
title: Implantando o JDBC Driver
description: Saiba como você pode redistribuir e implantar o Microsoft JDBC Driver para SQL Server com seu aplicativo e quais arquivos são necessários.
ms.custom: ''
ms.date: 03/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c99a7e4f491f2c00dc860ed85c453415f993593
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728362"
---
# <a name="deploying-the-jdbc-driver"></a>Implantando o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Ao implantar um aplicativo que depende do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você deve redistribuir o driver JDBC junto com o aplicativo. Diferentemente do Windows Data Access Components (Windows DAC) que é um componente do sistema operacional Windows, o driver JDBC é considerado um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Há duas abordagens para implantar o driver JDBC com o seu aplicativo. Uma é incluir os arquivos do driver JDBC como parte do seu próprio pacote de instalação personalizado. A segunda abordagem envolve o uso do pacote de instalação do JDBC fornecido pela Microsoft, que pode ser baixado da página de download [Driver do Microsoft JDBC para SQL Server](download-microsoft-jdbc-driver-for-sql-server.md).  
  
As seções a seguir discutem como usar o pacote de instalação do JDBC nos sistemas operacionais Windows e UNIX.  
  
> [!NOTE]  
> Para obter informações sobre como implantar aplicativos Java em geral, consulte o site de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implantando o JDBC Driver em sistemas Windows

Ao implantar o JDBC Driver em sistemas operacionais Windows será necessário desempacotar o pacote de instalação compactado, normalmente chamado de `sqljdbc_<version>_<language>.zip`.

## <a name="deploying-the-driver-on-unix-systems"></a>Implantando o driver em sistemas UNIX

Ao implantar o driver JDBC em sistemas operacionais UNIX, é necessário usar a versão do arquivo gzip do pacote de instalação, geralmente chamado `sqljdbc_<version>_<language>.tar.gz`.  
  
Antes de instalar o driver JDBC, verifique se ambos os utilitários, gzip e tar, estão instalados no sistema do usuário, e se as pastas que contêm os executáveis de ambos os utilitários foram adicionadas à variável de ambiente PATH.  
  
Para desempacotar o arquivo tar compactado, navegue até o diretório onde você deseja que o driver seja desempacotado e digite o seguinte comando:  
  
`gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
Para desempacotar o arquivo tar, mova-o para o diretório onde você deseja que o driver seja instalado e digite o seguinte comando:  
  
`tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>Legalidades de redistribuição de driver

As versões 6.0, 6.2, 6.4, 7.0, 7.2, 7.4 e 8.2 do JDBC Driver são redistribuíveis. Confira a cláusula sobre _Código Distribuível_ nos contratos de licença.

As versões 4.x do JDBC Driver são antigas e obsoletas. O suporte para as versões 4.x expirou antes de 2018.

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](overview-of-the-jdbc-driver.md)  
