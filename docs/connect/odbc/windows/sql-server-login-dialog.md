---
title: "Caixa de diálogo de logon do SQL Server (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 67aa8fc08a75efbcf77eb839b1999961a17e2a9f
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-login-dialog-box-odbc"></a>Caixa de diálogo Logon do SQL Server (ODBC)

Quando você chama uma conexão ODBC sem especificar informações suficientes para o driver para se conectar a um SQL Server, o ODBC driver exibe o **logon do SQL Server** caixa de diálogo.

## <a name="options"></a>Opções

### <a name="server"></a>Servidor

O nome de uma instância do SQL Server em sua rede. Selecione um nome de servidor \ instância na lista ou digite o nome de servidor \ instância no **Server** caixa. Opcionalmente, você pode criar um alias de servidor no computador cliente usando **SQL Server Configuration Manager**e digite esse nome de **Server** caixa.

Você pode digitar "(local)" quando você estiver usando o mesmo computador que o SQL Server. Em seguida, você pode se conectar a uma instância local do SQL Server, mesmo se estiver executando uma versão fora da rede do SQL Server.

Para obter mais informações sobre nomes de servidor para diferentes tipos de redes, consulte a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="authentication-mode"></a>Modo de Autenticação

Seleciona o modo de autenticação de um dos seguintes:
- **SQL Server** com ID de logon e senha
- **Integrada do Windows** autenticação usando a conta do usuário conectado no momento
- **Senha do Active Directory** com ID de logon e senha
- **Integrado ao Active Directory** autenticação usando a conta do usuário conectado no momento

Consulte [dados fonte Assistente tela 2](../../../connect/odbc/windows/dsn-wizard-2.md) para obter mais informações sobre os modos de autenticação.

### <a name="server-spn"></a>SPN do servidor

Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.

### <a name="login-id"></a>ID de Logon

Especifica a ID de logon do SQL Server ou do Active Directory do Azure a ser usado para a conexão se **modo de autenticação** é definido como **do SQL Server** ou **senha do Active Directory**. Caso contrário, o **ID de logon** caixa está desabilitada.

### <a name="password"></a>Senha

Especifica a senha para a ID de logon do SQL Server ou do Active Directory do Azure usada para a conexão se **modo de autenticação** é definido como **do SQL Server** ou **senhadoActiveDirectory**. Caso contrário, o **senha** caixa está desabilitada.

### <a name="options"></a>Opções

Exibe ou oculta o **opções** grupo. O **opções** botão é habilitado se **Server** tem um valor.

### <a name="change-password"></a>Alterar Senha

Quando essa caixa é selecionada, exibe o **nova senha** e **Confirmar nova senha** caixas.

### <a name="new-password"></a>Nova Senha

Especifica a nova senha.

### <a name="confirm-new-password"></a>Confirmar Nova Senha

Especifica a nova senha uma segunda vez, para confirmação.

### <a name="database"></a>Banco de Dados

Especifica o banco de dados padrão a ser usado na conexão. Essa configuração substitui o banco de dados padrão especificado para o logon no servidor. Se nenhum banco de dados for especificado, a conexão usará o banco de dados padrão especificado para o logon no servidor.

### <a name="mirror-server"></a>Servidor espelho

Especifica o nome do parceiro de failover do banco de dados a ser espelhado.

### <a name="mirror-spn"></a>SPN do espelho

Se desejar, especifique um SPN para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.

### <a name="language"></a>Idioma

Especifica o idioma nacional a ser usado para mensagens de sistema do SQL Server. O computador executando o SQL Server deve ter o idioma instalado. Essa configuração substitui o idioma padrão especificado para o logon no servidor. Se nenhum idioma for especificado, a conexão usará o idioma padrão especificado para o logon no servidor.

### <a name="application-name"></a>Nome do Aplicativo

(Opcional) Especifica o nome do aplicativo a ser armazenado na **program_name** coluna na linha para essa conexão em **sys. sysprocesses**.

### <a name="workstation-id"></a>ID da Estação de Trabalho

(Opcional) Especifica a ID de estação de trabalho a ser armazenado na **hostname** coluna na linha para essa conexão em **sys. sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Usar criptografia forte para dados

Quando selecionada, os dados que são passados por meio de conexão serão criptografados. Os logons são criptografados por padrão, até mesmo quando a caixa de seleção está desmarcada.

### <a name="trust-server-certificate"></a>Certificado do servidor confiável

Essa opção é aplicável somente quando **usar criptografia forte para dados** está habilitado. Quando selecionada, o certificado do servidor não será validado para que o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.

## <a name="see-also"></a>Consulte também

[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)

