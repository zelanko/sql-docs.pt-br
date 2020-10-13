---
title: Instalando o Assistente de Migração do SQL Server para acesso (AccessToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação do Assistente de Migração do SQL Server (SSMA) para acesso e como instalar, licenciar, atualizar e desinstalar.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1313699a3d82e0dbced8469f251a0a105f296246
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985182"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalando o Assistente de Migração do SQL Server para acesso (AccessToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O assistente de migração (SSMA) para acesso é instalado usando um assistente baseado em Windows Installer. Este tópico fornece informações sobre os pré-requisitos de instalação, um link para a versão mais recente do SSMA e instruções para instalar, licenciar, desinstalar e atualizar o SSMA.

## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar o SSMA, verifique se o seu sistema atende aos seguintes requisitos:

- Windows 7 ou uma versão posterior, ou Windows Server 2008 ou uma versão posterior.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] versão .NET Framework 4.7.2 ou posterior. O .NET Framework está disponível no [Guia de Microsoft .net](/dotnet/framework/).
- Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] para a qual você migrará objetos de banco de dados e data.
- Provedor DAO (Microsoft Data Access Object) versão 12,0 ou 14,0. Você pode instalar o provedor DAO do produto Microsoft Office 2010/2007 ou baixá-lo do site da Microsoft.
- 4 GB de RAM (recomendado).

## <a name="installing-ssma"></a>Instalar o SSMA

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaforaccess).

> [!IMPORTANT]
> Desinstale todas as versões anteriores do SSMA para acesso antes de instalar a nova versão.

Para instalar o SSMA:
  
1. Clique duas vezes em **SSMAforAccess_*n*. msi**, em que *n* é o número da compilação.
2. Na página Bem-vindo , clique em **Avançar**.

   Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.

3. Ler o contrato de licença de End-User; Se você concordar, selecione **aceito o contrato**e clique em **Avançar**.
4. Na página **escolher tipo de instalação** , clique em **típico**.
5. Na página **pronto para instalar** , você pode habilitar ou desabilitar a telemetria e as verificações de atualização automática toda vez que a ferramenta for iniciada. Clique em **Instalar** para iniciar a instalação.
  
O local de instalação padrão é `C:\Program Files\Microsoft SQL Server Migration Assistant for Access`.

## <a name="uninstalling-ssma-for-access"></a>Desinstalando o SSMA para acesso

Desinstale o SSMA usando **Adicionar ou remover programas** no painel de controle. Lembre-se de que a desinstalação do programa não exclui arquivos de projeto ou arquivos de log do SSMA.

Para desinstalar o SSMA:

1. Clique em **Iniciar**, clique em **Painel de Controle** e clique em **Adicionar ou Remover Programas**.
2. Selecione **Assistente de migração do Microsoft SQL Server para acesso**e clique em **remover**.

## <a name="upgrading-to-a-later-version"></a>Atualizando para uma versão posterior

Se você quiser atualizar para uma versão posterior do SSMA para Access, primeiro você deve desinstalar o SSMA para acesso e, em seguida, instalar a versão mais recente. Siga as instruções na seção desinstalando o SSMA para acesso para concluir este processo.

Se você abrir um projeto criado em uma versão anterior do SSMA para acesso, o SSMA poderá perguntar se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.

## <a name="see-also"></a>Veja também

- [Preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)
- [Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
- [Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)