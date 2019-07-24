---
title: Caixa de diálogo SQL Server logon (ODBC) | Microsoft Docs
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
ms.openlocfilehash: fcfde122b978fa1e77baa690a1f3e09417dab1c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989424"
---
# <a name="sql-server-login-dialog-box-odbc"></a>Caixa de diálogo Logon do SQL Server (ODBC)

Quando você chama uma conexão ODBC sem especificar informações suficientes para que o driver se conecte a um SQL Server, o driver ODBC exibe a caixa de diálogo **Logon do SQL Server**.

## <a name="options"></a>Opções

### <a name="server"></a>Servidor

O nome de uma instância do SQL Server em sua rede. Selecione um nome de servidor\instância na lista ou digite o nome do servidor\instância na caixa **Servidor**. Se desejar, crie um alias de servidor no computador cliente usando o **SQL Server Configuration Manager** e digite esse nome na caixa **Servidor**.

Digite "(local)" quando estiver usando o mesmo computador como SQL Server. Assim, você pode se conectar a uma instância local do SQL Server, até mesmo ao executar uma versão não em rede do SQL Server.

Para obter mais informações sobre nomes de servidor para diferentes tipos de rede, confira a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="authentication-mode"></a>Modo de Autenticação

Seleciona o modo de autenticação de um dos seguintes:
- **SQL Server** com ID de logon e senha
- Autenticação **integrada do Windows** usando a conta do usuário conectado no momento
- **Active Directory senha** com ID de logon e senha
- **Active Directory autenticação integrada** usando a conta do usuário conectado no momento
- Autenticação **Interativa do Active Directory** com ID de logon

Consulte a [tela 2 do assistente de fonte de dados](../../../connect/odbc/windows/dsn-wizard-2.md) para obter mais informações sobre os modos de autenticação.

### <a name="server-spn"></a>SPN do servidor

Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon SQL Server ou Azure Active Directory a ser usada para a conexão se o **modo de autenticação** estiver definido como **SQL Server** ou **Active Directory senha** ou **Active Directory interativo**. Caso contrário, a caixa **ID de logon** será desabilitada.

### <a name="password"></a>Senha

Especifica a senha para a ID de logon SQL Server ou Azure Active Directory usada para a conexão se o **modo de autenticação** estiver definido como **SQL Server** ou **Active Directory senha**. Caso contrário, a caixa **senha** será desabilitada.

### <a name="options"></a>Opções

Exibe ou oculta o grupo **Opções**. O botão **Opções** será habilitado se **Servidor** tiver um valor.

### <a name="change-password"></a>Alterar Senha

Quando essa caixa está selecionada, exibe as caixas **Nova Senha** e **Confirmar Nova Senha**.

### <a name="new-password"></a>Nova Senha

Especifica a nova senha.

### <a name="confirm-new-password"></a>Confirmar Nova Senha

Especifica a nova senha uma segunda vez, para confirmação.

### <a name="database"></a>banco de dados

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

Quando selecionado, os dados que são passados pela conexão serão criptografados. Os logons são criptografados por padrão, até mesmo quando a caixa de seleção está desmarcada.

### <a name="trust-server-certificate"></a>Confiar em certificado do servidor

Essa opção é aplicável somente quando o **uso de criptografia forte para dados** está habilitado. Quando selecionado, o certificado do servidor não será validado para ter o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.

## <a name="see-also"></a>Consulte Também

[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
