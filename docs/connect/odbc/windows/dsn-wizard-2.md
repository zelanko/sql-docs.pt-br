---
title: Tela 2 do assistente de fonte de dados (driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
ms.openlocfilehash: c997dd30b6d1e9844843ff4fa626c46b42fed463
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936580"
---
# <a name="data-source-wizard-screen-2"></a>Tela 2 do Assistente de Fonte de Dados

Especifique o método de autenticação, configure entradas de cliente avançadas do Microsoft SQL Server e o logon e a senha que o driver ODBC para SQL Server usará para se conectar ao SQL Server durante a configuração da fonte de dados.

## <a name="options"></a>Opções

### <a name="with-integrated-windows-authentication"></a>Com Autenticação Integrada do Windows

Especifica que o driver solicita uma conexão segura (ou confiável) com um SQL Server. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada para estabelecer conexões utilizando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor. Qualquer ID de logon ou senha fornecida é ignorada. O administrador do sistema SQL Server deve ter associado seu logon do Windows com uma ID de logon SQL Server (por exemplo, usando SQL Server Management Studio).

Se desejar, você pode especificar um SPN (nome da entidade de serviço) do servidor.

### <a name="with-active-directory-integrated-authentication"></a>Com Autenticação Integrada do Active Directory

Especifica que o driver é autenticado para SQL Server usando Azure Active Directory. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada do Azure Active Directory para estabelecer uma conexão usando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor.

### <a name="with-sql-server-authentication"></a>Com autenticação do SQL Server

Especifica que o driver é autenticado para SQL Server usando uma ID de logon e senha.

### <a name="with-active-directory-password-authentication"></a>Com autenticação de senha do Active Directory

Especifica que o driver se autentica para SQL Server usando uma ID de logon Azure Active Directory e uma senha.

### <a name="with-active-directory-interactive-authentication"></a>Com autenticação interativa do Active Directory

Especifica que o driver é autenticado para SQL Server usando Azure Active Directory modo interativo fornecendo a ID de logon. Isso irá disparar a caixa de diálogo de prompt de autenticação do Windows Azure.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon que o driver usa ao se conectar a SQL Server se **com SQL Server autenticação usando uma ID de logon e senha inseridos pelo usuário** ou **com Active Directory autenticação de senha usando uma ID de logon e senha digitadas pelo usuário** ou **com Active Directory autenticação interativa usando uma ID de logon inserida pelo usuário** está selecionada. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da fonte de dados após sua criação.

### <a name="password"></a>Senha

Especifica a senha que o driver usa ao se conectar a SQL Server se **com a autenticação SQL Server usando uma ID de logon e senha inseridos pelo usuário** ou **com Active Directory autenticação de senha usando uma ID de logon e senha digitadas pelo usuário** está selecionado. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da nova fonte de dados.

As caixas **ID de logon** e **senha** serão desabilitadas se **com a autenticação integrada do Windows** ou **com Active Directory autenticação integrada** estiver selecionada.

### <a name="next"></a>Próximo

Prossegue para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna à tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 1 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-1.md)

[Tela 3 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-3.md)

