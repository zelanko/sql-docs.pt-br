---
title: Instalando o Assistente de migração do SQL Server para Access (AccessToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f8dd4dcfc08366e78f11fc8b10fa269f17bb09e6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708434"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalando o Assistente de migração do SQL Server para Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migração Assistant (SSMA) para Access é instalado usando um assistente baseado no Windows Installer. Este tópico fornece informações sobre os pré-requisitos de instalação, um link para a versão mais recente do SSMA e instruções de instalação, licenciamento, desinstalação e atualização SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar o SSMA, certifique-se de que seu sistema atende aos seguintes requisitos:  
  
-   Windows 7 ou posterior, ou Windows Server 2008 ou posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versão 4.0 ou posterior. O .NET Framework versão 4.0 está disponível na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do produto e usando informações em de [guia do Microsoft .NET](https://docs.microsoft.com/dotnet/framework/).
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]banco de dados do SQL Azure para o qual você estará migrando dados e objetos de banco de dados.  
  
-   Microsoft Data Access Object (DAO) versão 12.0 ou 14.0 do provedor. Você pode instalar o provedor do DAO do produto do Microsoft Office 2010/2007 ou baixá-lo do site da Microsoft.  
  
-   O SQL Server Native Access Client (SNAC) versão 10.5 e posteriores para migração para o SQL Azure. Você pode obter a versão mais recente do SNAC de [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmaforaccess).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.

> [!IMPORTANT]  
> -   Desinstale todas as versões anteriores do SSMA para Access antes de instalar a nova versão.  
  
**Para instalar o SSMA**  
  
1.  Clique duas vezes no SSMA para Access *n*. msi, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próxima**.  
  
    Se você não tiver os pré-requisitos instalados, aparecerá uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença do usuário final; Se você concordar, marque **aceito o contrato**e, em seguida, clique em **próxima**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant for Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalando o SSMA para Access  
Desinstale o SSMA usando **adicionar ou remover programas** no painel de controle. Lembre-se de que desinstalar o programa não excluir os arquivos de projeto do SSMA ou arquivos de log.  
  
**Para desinstalar o SSMA**  
  
1.  Clique em **inicie**, clique em **painel de controle**e, em seguida, clique em **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant for Access**e, em seguida, clique em **remover**.  
  
## <a name="upgrading-to-a-later-version"></a>Atualizar para uma versão posterior  
Se você quiser atualizar para uma versão posterior do SSMA para Access, você deve primeiro desinstalar o SSMA para Access e, em seguida, instale a versão mais recente. Siga as instruções na desinstalação do SSMA para a seção acesso para concluir esse processo.  
  
Se você abrir um projeto criado em uma versão anterior do SSMA para Access, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="see-also"></a>Confira também  
[Preparar bancos de dados de acesso para a migração](preparing-access-databases-for-migration-accesstosql.md)  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vincular aplicativos do Access para o SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
