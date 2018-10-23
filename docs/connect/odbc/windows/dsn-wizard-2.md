---
title: Tela 2 (Driver ODBC para SQL Server) do Assistente de fonte de dados | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7d352b02d118c3de14cd437daf012885d7491c1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639514"
---
# <a name="data-source-wizard-screen-2"></a>Tela 2 do Assistente de Fonte de Dados

Especifique o método de autenticação, configure entradas de cliente avançadas do Microsoft SQL Server e o logon e a senha que o driver ODBC para SQL Server usará para se conectar ao SQL Server durante a configuração da fonte de dados.

## <a name="options"></a>Opções

### <a name="with-integrated-windows-authentication"></a>Com Autenticação Integrada do Windows

Especifica que o driver solicita uma conexão segura (ou confiável) para o SQL Server. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada para estabelecer conexões utilizando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor. Qualquer ID de logon ou senha fornecida é ignorada. O administrador do sistema do SQL Server deve ter associado seu logon do Windows com uma ID de logon do SQL Server (por exemplo, usando o SQL Server Management Studio).

Se desejar, você pode especificar um SPN (nome da entidade de serviço) do servidor.

### <a name="with-active-directory-integrated-authentication"></a>Com Autenticação Integrada do Active Directory

Especifica que o driver autenticar para o SQL Server usando o Azure Active Directory. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada do Azure Active Directory para estabelecer uma conexão usando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor.

### <a name="with-sql-server-authentication"></a>Com autenticação do SQL Server

Especifica se o driver se autenticar no SQL Server usando uma ID de logon e senha.

### <a name="with-active-directory-password-authentication"></a>Com autenticação de senha do Active Directory

Especifica que o driver autenticar para o SQL Server usando uma ID de logon do Active Directory do Azure e a senha.

### <a name="with-active-directory-interactive-authentication"></a>Com autenticação interativa do Active Directory

Especifica que o driver autenticar para o SQL Server usando o modo do Azure Active Directory Interactive, fornecendo a ID de logon. Isso vai disparar a caixa de diálogo de aviso de autenticação do Windows Azure.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon, o driver usa ao se conectar ao SQL Server, se **com autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** ou **autenticação com senha do Active Directory usando uma ID de logon e a senha inserida pelo usuário** ou **autenticação com o Active Directory Interactive usando uma ID de logon inserida pelo usuário** está selecionado. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da fonte de dados após sua criação.

### <a name="password"></a>Senha

Especifica a senha que o driver usa ao se conectar ao SQL Server, se **com autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** ou **autenticação com senha do Active Directory usando uma ID de logon e a senha inserida pelo usuário** está selecionado. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da nova fonte de dados.

Os dois os **ID de logon** e **senha** caixas serão desabilitadas se **autenticação integrada Windows com** ou **com integrado ao Active Directory autenticação** está selecionado.

### <a name="next"></a>Próximo

Continua para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 1 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-1.md)

[Tela 3 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-3.md)

