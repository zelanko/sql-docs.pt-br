---
title: Instalando o Assistente de Migração do SQL Server para acesso (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 80fc19b17ac1c01f0c57d828a3bc4821050f761d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257888"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalando o Assistente de Migração do SQL Server para acesso (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O assistente de migração (SSMA) para acesso é instalado usando um assistente baseado em Windows Installer. Este tópico fornece informações sobre os pré-requisitos de instalação, um link para a versão mais recente do SSMA e instruções para instalar, licenciar, desinstalar e atualizar o SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar o SSMA, verifique se o seu sistema atende aos seguintes requisitos:  
  
-   Windows 7 ou uma versão posterior, ou Windows Server 2008 ou uma versão posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame_md.md)] versão .NET Framework 4,0 ou posterior. A versão 4,0 do .NET Framework está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disco do produto e usando as informações no [Guia de Microsoft .net](https://docs.microsoft.com/dotnet/framework/).
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]BD/SQL do Azure para o qual você migrará objetos e dados de banco de dados.  
  
-   Provedor DAO (Microsoft Data Access Object) versão 12,0 ou 14,0. Você pode instalar o provedor DAO do produto Microsoft Office 2010/2007 ou baixá-lo do site da Microsoft.  
  
-   O cliente do SQL Server Native Access (SNAC) versão 10,5 e superior para migração para SQL Azure. Você pode obter a versão mais recente do SNAC do [Microsoft® SQL Server® 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaforaccess).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação do antes de poder instalar o SSMA.

> [!IMPORTANT]  
> -   Desinstale todas as versões anteriores do SSMA para acesso antes de instalar a nova versão.  
  
**Para instalar o SSMA**  
  
1.  Clique duas vezes em SSMA para Access *n*. msi, em que *n* é o número da compilação.  
  
2.  Na página de Boas-vindas, clique em **Avançar**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.  
  
3.  Ler o contrato de licença de usuário final; Se você concordar, selecione **aceito o contrato**e clique em **Avançar**.  
  
4.  Na página escolher tipo de instalação, clique em **típico**.  
  
5.  Clique em **Instalar**.  
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server for Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalando o SSMA para acesso  
Desinstale o SSMA usando **Adicionar ou remover programas** no painel de controle. Lembre-se de que a desinstalação do programa não exclui arquivos de projeto ou arquivos de log do SSMA.  
  
**Para desinstalar o SSMA**  
  
1.  Clique em **Iniciar**, clique em **Painel de Controle** e clique em **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para acesso**e clique em **remover**.  
  
## <a name="upgrading-to-a-later-version"></a>Atualizando para uma versão posterior  
Se você quiser atualizar para uma versão posterior do SSMA para Access, primeiro você deve desinstalar o SSMA para acesso e, em seguida, instalar a versão mais recente. Siga as instruções na seção desinstalando o SSMA para acesso para concluir este processo.  
  
Se você abrir um projeto criado em uma versão anterior do SSMA para acesso, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="see-also"></a>Confira também  
[Preparar bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
