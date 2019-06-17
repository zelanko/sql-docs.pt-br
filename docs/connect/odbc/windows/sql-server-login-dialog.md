---
title: Caixa de diálogo de logon do SQL Server (ODBC) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2d7cf1f31ce5cf42b9c2e4c7b72938b8def2ed4f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797737"
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
- **Integrada do Windows** autenticação usando a conta do usuário conectado no momento
- **Senha do Active Directory** com ID de logon e senha
- **Integrado ao Active Directory** autenticação usando a conta do usuário conectado no momento
- Autenticação **Interativa do Active Directory** com ID de logon

Ver [dados de origem Assistente tela 2](../../../connect/odbc/windows/dsn-wizard-2.md) para obter mais informações sobre os modos de autenticação.

### <a name="server-spn"></a>SPN do servidor

Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon do SQL Server ou do Active Directory do Azure a ser usado para a conexão se **modo de autenticação** é definido como **SQL Server** ou **senha do Active Directory** ou **Interativa do Active Directory**. Caso contrário, o **ID de logon** caixa está desabilitada.

### <a name="password"></a>Senha

Especifica a senha para a ID de logon do SQL Server ou o Azure Active Directory usada para a conexão se **modo de autenticação** é definido como **SQL Server** ou **senhadoActiveDirectory**. Caso contrário, o **senha** caixa está desabilitada.

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

Quando selecionada, os dados que são passados por meio de conexão serão criptografados. Os logons são criptografados por padrão, até mesmo quando a caixa de seleção está desmarcada.

### <a name="trust-server-certificate"></a>Confiar em certificado do servidor

Essa opção é aplicável somente quando **usar criptografia forte para dados** está habilitado. Quando selecionada, o certificado do servidor não será validado para que o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.

## <a name="see-also"></a>Consulte Também

[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
