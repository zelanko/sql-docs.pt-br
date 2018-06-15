---
title: Implantando o Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43a561de7ba1e47dc9b920c3a1459d38387620d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829571"
---
# <a name="deploying-the-jdbc-driver"></a>Implantando o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você implanta um aplicativo que depende de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você deve redistribuir o driver JDBC junto com seu aplicativo. Diferentemente do Windows Data Access Components (Windows DAC), que é um componente do sistema operacional Windows, o driver JDBC é considerado um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
 Há duas abordagens para implantar o driver JDBC com o seu aplicativo. Uma é incluir os arquivos do driver JDBC como parte do seu próprio pacote de instalação personalizado. A segunda abordagem envolve usando o pacote de instalação do JDBC fornecido pela Microsoft, que pode ser baixado no [Microsoft JDBC Driver para SQL Server Developer Center](http://go.microsoft.com/fwlink/?LinkId=70166).  
  
 As seções a seguir discutem como usar o pacote de instalação do JDBC nos sistemas operacionais Windows e UNIX.  
  
> [!NOTE]  
>  Para obter informações sobre como implantar aplicativos Java em geral, consulte o site de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implantando o driver JDBC em sistemas Windows  
 Quando você implantar o driver JDBC em sistemas operacionais Windows, você deve usar a versão do arquivo zip executável do pacote de instalação, geralmente denominado `sqljdbc_<version>_<language>.exe`.  
  
 Para executar o arquivo zip executável silenciosamente, você deve usar o `/auto` opção de linha de comando na linha de comando ou em um arquivo em lotes, como no exemplo a seguir:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Quando você usa o `/auto` opção não é uma instalação realmente silenciosa, pois uma caixa de diálogo do WinZip ainda é exibida na tela do usuário. No entanto, não é necessário interagir com ela, que é fechada assim que a operação de descompactação é concluída.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Implantando o driver em sistemas UNIX  
 Quando você implantar o driver JDBC em sistemas operacionais UNIX, você deve usar a versão do arquivo gzip do pacote de instalação, geralmente denominado `sqljdbc_<version>_<language>.tar.gz`.  
  
 Antes de instalar o driver JDBC, verifique se ambos os utilitários, gzip e tar, estão instalados no sistema do usuário, e se as pastas que contêm os executáveis de ambos os utilitários foram adicionadas à variável de ambiente PATH.  
  
 Para desempacotar o arquivo tar compactado, navegue até o diretório onde você deseja que o driver seja desempacotado e digite o seguinte comando:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Para desempacotar o arquivo tar, mova-o para o diretório onde você deseja que o driver seja instalado e digite o seguinte comando:  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
