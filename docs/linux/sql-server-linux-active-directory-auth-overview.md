---
title: Autenticação do Active Directory para o SQL Server no Linux | Microsoft Docs
description: Este artigo fornece uma visão geral da autenticação do Active Directory para o SQL Server no Linux.
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.workload: On Demand
ms.openlocfilehash: bd4ba9f12b7567f618db2aef1adb87a8f1f080f5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticação do Active Directory para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece uma visão geral da autenticação do Active Directory (AD) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Autenticação do AD também é conhecido como a autenticação integrada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

## <a name="ad-authentication-overview"></a>Visão geral de autenticação do AD

Autenticação do AD permite que os clientes de domínio no Windows ou Linux para autenticar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando suas credenciais de domínio e o protocolo Kerberos.

Autenticação do AD tem as seguintes vantagens sobre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação:

- Os usuários autenticados por meio de logon único, sem precisar inserir uma senha.   
- Ao criar logons para grupos do AD, você pode gerenciar o acesso e permissões em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando associações de grupo do AD.  
- Cada usuário tem uma única identidade na sua organização, para que você não precisa manter o controle de qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] logons correspondem às quais pessoas.   
- AD permite que você aplique uma política de senha centralizado na sua organização.   

## <a name="configuration-steps"></a>Etapas de configuração

Para usar a autenticação do Active Directory, você deve ter um controlador de domínio do AD (Windows) em sua rede.

Os detalhes sobre como configurar a autenticação do AD são fornecidos no tutorial, [Tutorial: autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md). A lista a seguir fornece um resumo com um link para cada seção do tutorial:

1. [Ingressar em um host do SQL Server para um domínio do Active Directory](sql-server-linux-active-directory-authentication.md#join).
1. [Crie um usuário do AD para o SQL Server e defina o ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurar o SQL Server service keytab](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Criar logons do SQL Server baseado no AD no Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Conecte-se ao SQL Server usando a autenticação do AD](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemas conhecidos

- Neste momento, o único método de autenticação com suporte para o ponto de extremidade de espelhamento de banco de dados é o certificado. Método de autenticação do WINDOWS será habilitado em uma versão futura.
- Ferramentas de terceiros do AD como Centrify, Powerbroker, e não há suporte para Vintela.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como implementar a autenticação do Active Directory para o SQL Server no Linux, consulte [Tutorial: autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).