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
ms.openlocfilehash: 860f4601e7ea3946ec3f8847033116864d7ed170
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632682"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalando o Assistente de Migração do SQL Server para acesso (AccessToSQL)
o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de Migração (SSMA) para acesso é instalado usando um assistente baseado em Windows Installer. Este tópico fornece informações sobre os pré-requisitos de instalação, um link para a versão mais recente do SSMA e instruções para instalar, licenciar, desinstalar e atualizar o SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Antes de instalar o SSMA, verifique se o seu sistema atende aos seguintes requisitos:  
  
-   Windows 7 ou uma versão posterior, ou Windows Server 2008 ou uma versão posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3,1 ou uma versão posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versão 4,0 ou posterior. A versão 4,0 do .NET Framework está disponível no disco do produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usando as informações no [guia Microsoft .net](https://docs.microsoft.com/dotnet/framework/).
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o banco de dados do Azure/SQL para o qual você migrará os objetos de banco de dados e os mesmos.  
  
-   Provedor DAO (Microsoft Data Access Object) versão 12,0 ou 14,0. Você pode instalar o provedor DAO do produto Microsoft Office 2010/2007 ou baixá-lo do site da Microsoft.  
  
-   O cliente do SQL Server Native Access (SNAC) versão 10,5 e superior para migração para SQL Azure. Você pode obter a versão mais recente do SNAC do [Microsoft® SQL Server® 2008 R2 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=16978)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaforaccess).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação do antes de poder instalar o SSMA.

> [!IMPORTANT]  
> -   Desinstale todas as versões anteriores do SSMA para acesso antes de instalar a nova versão.  
  
**Para instalar o SSMA**  
  
1.  Clique duas vezes em SSMA para Access *n*. msi, em que *n* é o número da compilação.  
  
2.  Na página de boas-vindas, clique em **Avançar**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.  
  
3.  Ler o contrato de licença de usuário final; Se você concordar, selecione **aceito o contrato**e clique em **Avançar**.  
  
4.  Na página escolher tipo de instalação, clique em **típico**.  
  
5.  Clique em **Instalar**.  
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server for Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalando o SSMA para acesso  
Desinstale o SSMA usando **Adicionar ou remover programas** no painel de controle. Lembre-se de que a desinstalação do programa não exclui arquivos de projeto ou arquivos de log do SSMA.  
  
**Para desinstalar o SSMA**  
  
1.  Clique em **Iniciar**, em **painel de controle**e em **Adicionar ou remover programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para acesso**e clique em **remover**.  
  
## <a name="upgrading-to-a-later-version"></a>Atualizando para uma versão posterior  
Se você quiser atualizar para uma versão posterior do SSMA para Access, primeiro você deve desinstalar o SSMA para acesso e, em seguida, instalar a versão mais recente. Siga as instruções na seção desinstalando o SSMA para acesso para concluir este processo.  
  
Se você abrir um projeto criado em uma versão anterior do SSMA para acesso, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="see-also"></a>Consulte também  
[Preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
