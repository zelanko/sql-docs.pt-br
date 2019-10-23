---
title: Configuração de Universal Data Link (UDL) | Microsoft Docs
description: Configuração de Universal Data Link (UDL) usando o driver de OLE DB da Microsoft para SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d92555fba1d9e0a380ffdc9051817ddfae9ca4b7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381756"
---
# <a name="universal-data-link-udl-configuration"></a>Configuração do UDL (Universal Data Link)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Guia conexão
Use a guia conexão para especificar como se conectar aos seus dados usando o driver do Microsoft OLE DB para SQL Server.

![Captura de tela de páginas de link de dados OLE DB-guia conexão](../media/data-link-pages-connection-tab.png)

A guia Conexão é específica do provedor e exibe apenas as propriedades de conexão necessárias ao Microsoft OLE DB Driver para SQL Server.

|Opção|Descrição|
|---   |---        |
|Selecione ou digite um nome de servidor|selecione um nome de servidor na lista suspensa ou digite o local do servidor em que o banco de dados que você deseja acessar está localizado. Selecionar o banco de dados no servidor é uma ação separada. Atualize a lista clicando em "Atualizar".
|Insira as informações para entrar no servidor|Você pode selecionar as seguintes opções de autenticação nesta lista suspensa: <ul><li>`Windows Authentication:` autenticação para SQL Server usando as credenciais de conta do Windows do usuário conectado no momento.</li><li>`SQL Server Authentication:` autenticação usando a ID de logon e a senha.</li><li>`Active Directory - Integrated:` autenticação integrada com uma identidade de Azure Active Directory. Esse modo também pode ser usado para a autenticação do Windows para SQL Server.</li><li>`Active Directory - Password:` a ID de usuário e a autenticação de senha com uma identidade de Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` a autenticação interativa com uma identidade de Azure Active Directory. Esse modo dá suporte à MFA (autenticação multifator) do Azure.</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|Nome de usuário|Digite a ID de usuário a ser usada para autenticação quando você entrar na fonte de dados.|
|Senha|Digite a senha a ser usada para autenticação quando você entrar na fonte de dados.|
|Senha em branco|Quando marcada, habilita o provedor especificado a usar uma senha em branco na cadeia de conexão.|
|Permitir Salvamento de Senha|Quando marcada, permite que a senha seja salva com a cadeia de conexão. Se a senha será incluída na cadeia de conexão dependerá da funcionalidade do aplicativo de chamada. <br/><br/>**OBSERVAÇÃO:** se salva, a senha é retornada e salva sem-máscara e sem-criptografia.|
|Usar criptografia forte para dados|Quando marcada, os dados passados pela conexão serão criptografados.|
|Confiar em certificado do servidor|Quando marcada, o certificado do servidor será validado. O certificado do servidor deve ter o nome de host correto do servidor e emitido por uma autoridade de certificação confiável.|
|Selecionar o banco de dados|Selecione ou digite o nome do banco de dados que você deseja acessar.|
|Anexar arquivo de BD como nome de banco de dados|Especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e usado como o banco de dados padrão da fonte de dados. Na primeira caixa de texto sob esta seção, digite o nome do banco de dados a ser usado para o arquivo de banco de dados anexado.<br/><br/>Digite o caminho completo até o arquivo de banco de dados a ser anexado na caixa de texto rotulada `Using the filename` ou clique no botão `...` para procurar o arquivo de banco de dados.|
|Alterar Senha|Exibe a caixa de diálogo Alterar SQL Server senha. |
|Testar Conexão|Clique para tentar uma conexão com a fonte de dados especificada. Se a conexão falhar, verifique se as configurações estão corretas. Por exemplo, erros ortográficos e diferenciação de maiúsculas e minúsculas podem causar falhas de conexão.|

## <a name="advanced-tab"></a>Guia Avançado
Use a guia Avançado para exibir e definir propriedades de inicialização adicionais.

![Captura de tela de páginas de link de dados OLE DB-guia Avançado](../media/data-link-pages-advanced-tab.png)

|Opção|Descrição|
|---   |---        |
| Tempo limite de conexão | Especifica a quantidade de tempo (em segundos) que o Microsoft OLE DB driver for SQL Server aguarda a conclusão da inicialização. Se o tempo limite da inicialização for alcançado, um erro será retornado e a conexão não será criada.|


> [!NOTE]  
>  Para obter informações gerais de conexão de link de dados, consulte a [visão geral da API de link de dados](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Próximas etapas
- [Autenticar para Azure Active Directory](../features/using-azure-active-directory.md) usando o driver OLE DB.

- [Solicitar credenciais de autenticação ao usuário](../help-topics/sql-server-login-dialog.md) usando o driver de OLE DB.