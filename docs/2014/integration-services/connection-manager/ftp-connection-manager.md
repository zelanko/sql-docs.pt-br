---
title: Gerenciador de conexões FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b22fbb63dda4b6e3211a5bb53cfd70e243e6960f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193606"
---
# <a name="ftp-connection-manager"></a>Gerenciador de conexões FTP
  Um gerenciador de conexões de FTP habilita um pacote a conectar-se a um servidor FTP. A tarefa FTP que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa esse gerenciador de conexões.  
  
 Quando você adiciona um gerenciador de conexões de FTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que pode ser resolvido como  uma conexão FTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção `Connections` do pacote.  
  
 O `ConnectionManagerType` propriedade do Gerenciador de conexão é definida como `FTP`.  
  
 Você pode configurar um gerenciador de conexões de FTP adotando um dos procedimentos a seguir:  
  
-   Especificando um nome e uma porta de servidor.  
  
-   Especificando o acesso anônimo ou fornecendo um nome de usuário e uma senha para autenticação básica.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
-   Definindo o tempo limite, o número de repetições e a quantidade de dados a ser copiada de cada vez.  
  
-   Indicando se o gerenciador de conexões de FTP usa modo passivo ou ativo.  
  
 Dependendo da configuração do site de FTP ao qual o gerenciador de conexões de FTP se conectar, será necessário alterar os seguintes valores padrão do gerenciador de conexões:  
  
-   A porta de servidor é definida como 21. Você deve especificar a porta que o site FTP escuta.  
  
-   O nome de usuário é definido como "anônimo". Você deve fornecer as credenciais exigidas pelo site FTP.  
  
## <a name="activepassive-modes"></a>Modos ativo/passivo  
 Um gerenciador de conexões de FTP pode enviar e receber arquivos usando o modo ativo ou passivo. No modo ativo, o servidor inicia a conexão de dados e, no modo passivo, o cliente inicia a conexão de dados.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>Configuração do gerenciador de conexões FTP  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte [Editor do Gerenciador de Conexões FTP](../ftp-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um Gerenciador de conexão programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa FTP](../control-flow/ftp-task.md)   
 [Serviços de integração &#40;SSIS&#41; conexões](integration-services-ssis-connections.md)  
  
  
