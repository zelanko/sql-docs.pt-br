---
title: "Instalando o Assistente de migração do SQL Server para Access (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: e93611af32e1317096fc2ea95f8b4d2147a88bcc
ms.contentlocale: pt-br
ms.lasthandoff: 08/16/2017

---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalando o Assistente de migração do SQL Server para Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para acesso é instalado usando um assistente baseado no Windows Installer. Este tópico fornece informações sobre os pré-requisitos de instalação, um link para a versão mais recente do SSMA e instruções para a instalação, licenciamento, desinstalar e atualizar SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Antes de instalar o SSMA, certifique-se de que seu sistema atende aos seguintes requisitos:  
  
-   Windows 7 ou posterior, ou Windows Server 2008 ou posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versão 4.0 ou posterior. O .NET Framework versão 4.0 está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] disco do produto e usando as informações a [guia do Microsoft .NET](https://docs.microsoft.com/en-us/dotnet/framework/).
  
-   Acesso e permissões suficientes no computador que hospeda a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ao qual você está fazendo a migração dados e objetos de banco de dados do SQL Azure DB.  
  
-   Microsoft Data Access Object (DAO) versão 12.0 ou 14.0 do provedor. Você pode instalar o provedor DAO de produto do Microsoft Office 2010/2007 ou baixá-lo do site da Microsoft.  
  
-   O SQL Server Native Access Client (SNAC) versão 10.5 e acima para a migração para o SQL Azure. Você pode obter a versão mais recente do SNAC de [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalando o SSMA  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmaforaccess).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.

> [!IMPORTANT]  
> -   Desinstale todas as versões anteriores do SSMA para Access antes de instalar a nova versão.  
  
**Para instalar o SSMA**  
  
1.  Clique duas vezes o SSMA para Access  *n* . msi, onde  *n*  é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próximo**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você tenha instalado todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença do usuário final; Se você concordar, selecione **aceito o contrato**e, em seguida, clique em **próximo**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant para acesso.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalando o SSMA para Access  
Desinstalar o SSMA usando **adicionar ou remover programas** no painel de controle. Lembre-se de que desinstalar o programa não excluir os arquivos de projeto SSMA ou arquivos de log.  
  
**Para desinstalar o SSMA**  
  
1.  Clique em **iniciar**, clique em **painel de controle**e, em seguida, clique em **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para acesso**e, em seguida, clique em **remover**.  
  
## <a name="upgrading-to-a-later-version"></a>Atualizar para uma versão posterior  
Se você quiser atualizar para uma versão posterior do SSMA para Access, você deve primeiro desinstalar o SSMA para Access e, em seguida, instale a versão mais recente. Siga as instruções na desinstalação do SSMA para a seção de acesso concluir este processo.  
  
Se você abrir um projeto criado em uma versão anterior do SSMA para Access, SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="see-also"></a>Consulte também  
[Preparar bancos de dados do Access para a migração](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Vinculando a aplicativos de acesso ao SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  

