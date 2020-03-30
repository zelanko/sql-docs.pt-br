---
title: Tela 2 do Assistente de Fonte de Dados (ODBC Driver for SQL Server) | Microsoft Docs
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
ms.openlocfilehash: 4ab8be02351a23c78251a99ca707e946ee8944c8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "70152563"
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

Especifica que o driver autentique-se com o SQL Server usando o modo interativo do Azure Active Directory, fornecendo uma ID de logon. Isso fará com que a caixa de diálogo de aviso da Autenticação do Azure apareça.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon que o driver usará ao se conectar ao SQL Server se uma das opções **Com a Autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário**, **Com a Autenticação de senha do Active Directory usando uma ID de logon e senha inseridos pelo usuário** e **Com a Autenticação interativa do Active Directory usando uma ID de logon inserida pelo usuário** estiver selecionada. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da fonte de dados após sua criação.

### <a name="password"></a>Senha

Especifica a senha que o driver usará ao se conectar ao SQL Server se uma das opções **Com a Autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** e **Com a Autenticação de senha do Active Directory usando uma ID de logon e senha inseridos pelo usuário** estiver selecionada. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da nova fonte de dados.

As caixas **ID de logon** e **Senha** serão desabilitadas se uma entre as opções **Com a Autenticação Integrada do Windows** e **Com a Autenticação integrada do Active Directory** estiver selecionada.

### <a name="next"></a>Próximo

Prossegue para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 1 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-1.md)

[Tela 3 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-3.md)

