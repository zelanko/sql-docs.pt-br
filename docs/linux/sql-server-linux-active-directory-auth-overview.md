---
title: Autenticação do Active Directory para o SQL Server em Linux
titleSuffix: SQL Server
description: Este artigo fornece uma visão geral da Autenticação do Active Directory para SQL Server em Linux.
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 32ff23fe1ea7f0a892a19cc6be0eef8439ee907f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75831823"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticação do Active Directory para o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece uma visão geral da autenticação do AD (Active Directory) para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. A autenticação do AD também é conhecida como Autenticação integrada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="ad-authentication-overview"></a>Visão geral da autenticação do AD

A autenticação do AD permite que clientes ingressados em domínio no Windows ou no Linux se autentiquem no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando suas credenciais de domínio e o protocolo Kerberos.

A Autenticação do AD tem as seguintes vantagens em relação à Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

- Os usuários autenticam-se por meio de logon único, sem a necessidade de fornecer uma senha.
- Ao criar logons para grupos do AD, é possível gerenciar o acesso e permissões no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando as associações aos grupos do AD.  
- Cada usuário tem uma única identidade em sua organização; portanto, você não precisa controlar quais logons do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] correspondem a quais pessoas.   
- O AD permite que você imponha uma política de senha centralizada em sua organização.

## <a name="configuration-steps"></a>Etapas de configuração

Para usar a autenticação do Active Directory, você deve ter um Controlador de Domínio do AD (Windows) em sua rede.

Os detalhes de como configurar a autenticação do AD são fornecidos no tutorial, [Tutorial: Use a autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md). A lista a seguir fornece um resumo com um link para cada seção no tutorial:

1. [Ingressar um host do SQL Server em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).
1. [Criar um usuário do AD para SQL Server e definir ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurar keytab do serviço SQL Server](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Proteger o arquivo keytab](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Configurar o SQL Server para usar o arquivo keytab para autenticação Kerberos](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Criar logons do SQL Server baseados em AD no Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Conectar-se ao SQL Server usando a autenticação do AD](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemas conhecidos

- Neste momento, o único método de autenticação com suporte do ponto de extremidade de espelhamento de banco de dados é CERTIFICATE. O método de autenticação WINDOWS será habilitado em uma versão futura.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como implementar a autenticação do Active Directory para SQL Server em Linux, confira [Tutorial: Use a autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md).
