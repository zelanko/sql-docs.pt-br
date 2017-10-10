---
title: Tela 2 (Driver ODBC para SQL Server) do Assistente de fonte de dados | Microsoft Docs
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e861bc52621e520a27e930dd22f1a1eb9613cc76
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-2"></a>Tela 2 do Assistente de Fonte de Dados

Especifique o método de autenticação e configurar entradas de cliente avançado do Microsoft SQL Server e o logon e a senha que o driver ODBC do SQL Server usará para se conectar ao SQL Server ao configurar a fonte de dados.

## <a name="options"></a>Opções

### <a name="with-integrated-windows-authentication"></a>Com a autenticação integrada do Windows

Especifica que o driver solicita uma conexão segura (ou confiável) com um SQL Server. Quando essa opção está selecionada, o SQL Server usa segurança de logon integrada para estabelecer conexões utilizando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor. Qualquer ID de logon ou senha fornecida é ignorada. O administrador do sistema do SQL Server deve ter associado seu logon do Windows com uma ID de logon do SQL Server (por exemplo, usando o SQL Server Management Studio).

Se desejar, você pode especificar um SPN (nome da entidade de serviço) do servidor.

### <a name="with-active-directory-integrated-authentication"></a>Com a autenticação integrada do Active Directory

Especifica que o driver se autenticar ao SQL Server usando o Active Directory do Azure. Quando selecionada, o SQL Server usa segurança de logon do Azure Active Directory integrado para estabelecer uma conexão usando essa fonte de dados, independentemente do modo de segurança de logon atual no servidor.

### <a name="with-sql-server-authentication"></a>Com a autenticação do SQL Server

Especifica que o driver se autenticar ao SQL Server usando uma ID de logon e senha.

### <a name="with-active-directory-password-authentication"></a>Com a autenticação de senha do Active Directory

Especifica que o driver autenticar usando uma ID de logon do Active Directory do Azure e a senha do SQL Server.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon que o driver usa ao se conectar ao SQL Server se **com autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** ou **autenticação com senha do Active Directory usando uma ID de logon e a senha inserida pelo usuário** está selecionado. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da fonte de dados após sua criação.

### <a name="password"></a>Senha

Especifica a senha que o driver usa ao se conectar ao SQL Server se **com autenticação do SQL Server usando uma ID de logon e senha inseridos pelo usuário** ou **autenticação com senha do Active Directory usando uma ID de logon e a senha inserida pelo usuário** está selecionado. Isso se aplica apenas à conexão estabelecida para determinar as configurações padrão do servidor; não se aplica às conexões seguintes feitas com o uso da nova fonte de dados.

Ambos os **ID de logon** e **senha** caixas serão desabilitadas se **com autenticação integrada do Windows** ou **com integrado ao Active Directory autenticação** está selecionado.

### <a name="next"></a>Próximo

Vai para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 1 do Assistente de fonte de dados](../../../connect/odbc/windows/dsn-wizard-1.md)

[Tela de Assistente de fonte de dados 3](../../../connect/odbc/windows/dsn-wizard-3.md)


