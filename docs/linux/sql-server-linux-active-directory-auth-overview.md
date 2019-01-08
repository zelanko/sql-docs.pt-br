---
title: Autenticação do Active Directory para o SQL Server no Linux
titleSuffix: SQL Server
description: Este artigo fornece uma visão geral da autenticação do Active Directory para o SQL Server no Linux.
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: fcc2148119634c7114d72f67b2c7143fa7d47724
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160394"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticação do Active Directory para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece uma visão geral da autenticação do Active Directory (AD) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Autenticação do AD também é conhecido como a autenticação integrada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

## <a name="ad-authentication-overview"></a>Visão geral de autenticação do AD

Autenticação do AD permite que os clientes ingressados no domínio no Windows ou Linux para se autenticar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando suas credenciais de domínio e o protocolo Kerberos.

Autenticação do AD tem as seguintes vantagens sobre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação:

- Os usuários autenticados por meio de logon único, sem inserir uma senha.   
- Ao criar logons para grupos do AD, você pode gerenciar o acesso e permissões no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando associações de grupo do AD.  
- Cada usuário tem uma única identidade na sua organização, para que você não precise manter o controle de quais [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] logons correspondem às quais as pessoas.   
- AD permite que você aplique uma política de senha centralizado em sua organização.   

## <a name="configuration-steps"></a>Etapas de configuração

Para usar autenticação do Active Directory, você deve ter um controlador de domínio do AD (Windows) em sua rede.

Os detalhes de como configurar a autenticação do AD são fornecidos no tutorial, [Tutorial: Usar autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md). A lista a seguir fornece um resumo com um link para cada seção do tutorial:

1. [Ingressar em um host do SQL Server em um domínio do Active Directory](sql-server-linux-active-directory-authentication.md#join).
1. [Criar um usuário do AD para o SQL Server e definir o ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurar o SQL Server service keytab](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Criar logons do SQL Server com base no AD no Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Conectar-se ao SQL Server usando a autenticação do AD](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemas conhecidos

- Neste momento, o único método de autenticação com suporte para o ponto de extremidade de espelhamento de banco de dados é o certificado. Método de autenticação do WINDOWS será habilitado em uma versão futura.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como implementar a autenticação do Active Directory para o SQL Server no Linux, consulte [Tutorial: Usar autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).
