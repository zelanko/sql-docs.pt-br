---
title: Usando o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b688e5b014915578df5c56ec5e6af2fc8fe26b16
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781975"
---
# <a name="deploying-the-jdbc-driver"></a>Implantando o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao implantar um aplicativo que depende do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você deve redistribuir o driver JDBC junto com o aplicativo. Diferentemente do Windows Data Access Components (Windows DAC) que é um componente do sistema operacional Windows, o driver JDBC é considerado um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Há duas abordagens para implantar o driver JDBC com o seu aplicativo. Uma é incluir os arquivos do driver JDBC como parte do seu próprio pacote de instalação personalizado. A segunda abordagem envolve o uso do pacote de instalação do JDBC fornecido pela Microsoft, que pode ser baixado no [Microsoft JDBC Driver para SQL Server Developer Center](https://go.microsoft.com/fwlink/?LinkId=70166).  
  
 As seções a seguir discutem como usar o pacote de instalação do JDBC nos sistemas operacionais Windows e UNIX.  
  
> [!NOTE]  
>  Para obter informações sobre como implantar aplicativos Java em geral, consulte o site de Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Implantando o driver JDBC em sistemas Windows  
 Ao implantar o driver JDBC em sistemas operacionais Windows, você deve usar a versão de arquivo zip executável do pacote de instalação, geralmente denominado `sqljdbc_<version>_<language>.exe`.  
  
 Para executar o arquivo zip executável silenciosamente, use a opção de linha de comando `/auto` ou um arquivo em lotes, como a seguir:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Quando a opção `/auto` é usada, a instalação não é realmente silenciosa, pois uma caixa de diálogo do WinZip ainda é exibida na tela do usuário. No entanto, não é necessário interagir com ela, que é fechada assim que a operação de descompactação é concluída.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Implantando o driver em sistemas UNIX  
 Ao implantar o driver JDBC em sistemas operacionais UNIX, é necessário usar a versão do arquivo gzip do pacote de instalação, geralmente chamado `sqljdbc_<version>_<language>.tar.gz`.  
  
 Antes de instalar o driver JDBC, verifique se ambos os utilitários, gzip e tar, estão instalados no sistema do usuário, e se as pastas que contêm os executáveis de ambos os utilitários foram adicionadas à variável de ambiente PATH.  
  
 Para desempacotar o arquivo tar compactado, navegue até o diretório onde você deseja que o driver seja desempacotado e digite o seguinte comando:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Para desempacotar o arquivo tar, mova-o para o diretório onde você deseja que o driver seja instalado e digite o seguinte comando:  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
