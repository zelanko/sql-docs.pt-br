---
description: Tela 2 do Assistente de Fonte de Dados (ODBC Driver for SQL Server)
title: Tela 2 do Assistente de Fonte de Dados (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: d1e18939ab9d3f2e86452dd3f1847971157ca92c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462205"
---
# <a name="data-source-wizard-screen-2"></a>Tela 2 do Assistente de Fonte de Dados

Especifique o método de autenticação, configure entradas de cliente avançadas do Microsoft SQL Server e o logon e a senha que o driver ODBC para SQL Server usará para se conectar ao SQL Server durante a configuração da fonte de dados.

## <a name="options"></a>Opções

### <a name="with-integrated-windows-authentication"></a>Com Autenticação Integrada do Windows

Especifica que o driver solicita uma conexão segura (ou confiável) com um SQL Server. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada para estabelecer conexões utilizando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor. Qualquer ID de logon ou senha fornecida é ignorada. O administrador do sistema do SQL Server deve ter associado seu logon do Windows a uma ID de logon do SQL Server (por exemplo, usando o SQL Server Management Studio).

Se desejar, você pode especificar um SPN (nome da entidade de serviço) do servidor.

### <a name="with-active-directory-integrated-authentication"></a>Com Autenticação Integrada do Active Directory

Especifica que o driver autentique-se com o SQL Server usando Azure Active Directory. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada do Azure Active Directory para estabelecer uma conexão usando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor.

### <a name="with-sql-server-authentication"></a>Com autenticação do SQL Server

Especifica que o driver autentique-se com o SQL Server usando uma ID de logon e uma senha.

### <a name="with-active-directory-password-authentication"></a>Com autenticação de senha do Active Directory

Especifica que o driver autentique-se com o SQL Server usando uma ID de logon e uma senha do Azure Active Directory.

### <a name="with-active-directory-interactive-authentication"></a>Com autenticação interativa do Active Directory

Especifica que o driver autentique-se com o SQL Server usando o modo interativo do Azure Active Directory, fornecendo uma ID de logon. Essa opção acionará a caixa de diálogo de prompt da Autenticação do Azure.

### <a name="with-managed-identity-authentication"></a>Com autenticação de Identidade Gerenciada

Especifica que o driver se autentica com o SQL Server usando uma Identidade Gerenciada.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon que o driver usará ao se conectar ao SQL Server se uma das opções **Com a Autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário**, **Com a Autenticação de senha do Active Directory usando uma ID de logon e senha inseridos pelo usuário** e **Com a Autenticação interativa do Active Directory usando uma ID de logon inserida pelo usuário** estiver selecionada. Se a opção **Com autenticação de Identidade Gerenciada** estiver selecionada, especifique a ID do objeto da identidade gerenciada ou deixe em branco para usar a identidade padrão. Esse campo se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; ele não se aplica às conexões subsequentes feitas com o uso da fonte de dados após sua criação, exceto ao usar a autenticação de Identidade Gerenciada.

### <a name="password"></a>Senha

Especifica a senha que o driver usará ao se conectar ao SQL Server se uma das opções **Com a Autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** e **Com a Autenticação de senha do Active Directory usando uma ID de logon e senha inseridos pelo usuário** estiver selecionada. Esse campo se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; ele não se aplica às conexões subsequentes feitas com o uso da nova fonte de dados.

As caixas **ID de logon** e **Senha** serão desabilitadas se uma entre as opções **Com a Autenticação Integrada do Windows** e **Com a Autenticação integrada do Active Directory** estiver selecionada.

### <a name="next"></a>Avançar

Prossegue para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 1 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-1.md)

[Tela 3 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-3.md)

