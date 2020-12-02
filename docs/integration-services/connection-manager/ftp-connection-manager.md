---
description: Gerenciador de conexões FTP
title: Gerenciador de conexões FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 854f975c64f5622c53d04c51651929d83745864a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91728037"
---
# <a name="ftp-connection-manager"></a>Gerenciador de conexões FTP

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões de FTP habilita um pacote a conectar-se a um servidor FTP. A tarefa FTP que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa esse gerenciador de conexões.  
  
 Quando você adiciona um gerenciador de conexões de FTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que pode ser resolvido como uma conexão FTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Conexões** do pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **FTP**.  
  
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
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte [Editor do Gerenciador de Conexões FTP]().  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="ftp-connection-manager-editor"></a>Editor do Gerenciador de Conexões FTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões FTP** para especificar as propriedades de conexão com um servidor FTP.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para saber mais sobre o gerenciador de conexões FTP, consulte [Gerenciador de Conexões FTP](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do servidor**  
 Forneça o nome do servidor FTP.  
  
 **Porta do servidor**  
 Especifique o número da porta no servidor FTP a ser usada na conexão. O valor padrão dessa propriedade é **21**.  
  
 **Nome de usuário**  
 Forneça um nome de usuário para acessar o servidor FTP. O valor padrão dessa propriedade é **anonymous**.  
  
 **Senha**  
 Forneça uma senha para acessar o servidor FTP.  
  
 **Tempo limite (em segundos)**  
 Especifique o número de segundos que a tarefa terá antes de exceder o tempo limite. O valor **0** indica um tempo infinito. O valor padrão dessa propriedade é **60**.  
  
 **Usar modo passivo**  
 Especifique se o servidor ou o cliente inicia a conexão. No modo ativo, o servidor inicia a conexão e, no modo passivo, o cliente ativa a conexão. O valor padrão dessa propriedade é **active mode**.  
  
 **Novas tentativas**  
 Especifique o número de vezes que a tarefa tenta fazer uma conexão. Um valor de **0** indica que não há limite ao número de tentativas.  
  
 **Tamanho da parte (em KB)**  
 Forneça um tamanho de parte em kilobytes para transmissão de dados.  
  
 **Testar Conexão**  
 Depois de configurar o Gerenciador de Conexões FTP, confirme se a conexão é viável clicando em **Testar Conexão**.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa FTP](../../integration-services/control-flow/ftp-task.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
