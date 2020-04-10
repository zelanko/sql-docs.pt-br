---
title: Caixa de diálogo Logon do SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: 35a9c6b6c254d6ed7c3283aedba15e65b6114579
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920122"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Caixa de diálogo Logon do SQL Server (ODBC)

Quando você chama uma conexão ODBC sem especificar informações suficientes para que o driver se conecte a um SQL Server, o driver ODBC exibe a caixa de diálogo **Logon do SQL Server**.

## <a name="options"></a>Opções

### <a name="server"></a>Servidor

O nome de uma instância do SQL Server na sua rede. Selecione um nome de servidor\instância na lista ou digite o nome do servidor\instância na caixa **Servidor**. Se desejar, crie um alias de servidor no computador cliente usando o **SQL Server Configuration Manager** e digite esse nome na caixa **Servidor**.

Digite "(local)" quando estiver usando o mesmo computador como SQL Server. Assim, você pode se conectar a uma instância local do SQL Server, até mesmo ao executar uma versão não em rede do SQL Server.

Para obter mais informações sobre nomes de servidor para diferentes tipos de rede, confira a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="authentication-mode"></a>Modo de autenticação

Selecione um dos seguintes modos de autenticação:
- **SQL Server** com ID de logon e senha
- Autenticação **Integrada do Windows** usando a conta do usuário autenticado atualmente
- **Senha do Active Directory** com ID de logon e senha
- Autenticação **Integrada do Active Directory** usando a conta do usuário autenticado atualmente
- Autenticação **Interativa do Active Directory** com ID de logon

Confira [Tela 2 do Assistente de fonte de dados](../../../connect/odbc/windows/dsn-wizard-2.md) para obter mais informações sobre os modos de autenticação.

### <a name="server-spn"></a>SPN do servidor

Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon do SQL Server ou do Azure Active Directory a ser usada para a conexão se **Modo de Autenticação** está definido como **SQL Server** ou **Senha do Active Directory** ou **Active Directory Interativo**. Caso contrário, a caixa **ID de Logon** será desabilitada.

### <a name="password"></a>Senha

Especifica a senha para a ID de logon do SQL Server ou do Azure Active Directory usada para a conexão se **Modo de Autenticação** está definido como **SQL Server** ou **Senha do Active Directory**. Caso contrário, a caixa **Senha** será desabilitada.

### <a name="options"></a>Opções

Exibe ou oculta o grupo **Opções**. O botão **Opções** será habilitado se **Servidor** tiver um valor.

### <a name="change-password"></a>Alterar Senha

Quando essa caixa está selecionada, exibe as caixas **Nova Senha** e **Confirmar Nova Senha**.

### <a name="new-password"></a>Nova senha

Especifica a nova senha.

### <a name="confirm-new-password"></a>Confirmar Nova Senha

Especifica a nova senha uma segunda vez, para confirmação.

### <a name="database"></a>Banco de dados

Especifica o banco de dados padrão a ser usado na conexão. Essa configuração substitui o banco de dados padrão especificado para o logon no servidor. Se nenhum banco de dados for especificado, a conexão usará o banco de dados padrão especificado para o logon no servidor.

### <a name="mirror-server"></a>Servidor Espelho

Especifica o nome do parceiro de failover do banco de dados a ser espelhado.

### <a name="mirror-spn"></a>SPN do espelho

Se desejar, especifique um SPN para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.

### <a name="language"></a>Linguagem

Especifica o idioma nacional a ser usado para mensagens de sistema do SQL Server. O computador que executa o SQL Server deve ter o idioma instalado. Essa configuração substitui o idioma padrão especificado para o logon no servidor. Se nenhum idioma for especificado, a conexão usará o idioma padrão especificado para o logon no servidor.

### <a name="application-name"></a>Nome do Aplicativo

(Opcional) Especifica o nome do aplicativo a ser armazenado na coluna **program_name** na linha dessa conexão em **sys.sysprocesses**.

### <a name="workstation-id"></a>ID da Estação de Trabalho

(Opcional) Especifica a ID da estação de trabalho a ser armazenada na coluna **hostname** na linha dessa conexão em **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Usar criptografia forte para dados

Quando selecionado, os dados transmitidos pela conexão serão criptografados. Os logons são criptografados por padrão, até mesmo quando a caixa de seleção está desmarcada.

### <a name="trust-server-certificate"></a>Confiar em certificado do servidor

Essa opção é aplicável somente quando a opção **Usar criptografia forte para dados** está habilitada. Quando essa opção estiver selecionada, o certificado do servidor não será validado para ter o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.

## <a name="see-also"></a>Consulte Também

[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
