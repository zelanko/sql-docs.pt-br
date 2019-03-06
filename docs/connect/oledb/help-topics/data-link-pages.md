---
title: Universal Data Link (UDL) configuração | Microsoft Docs
description: Configuração universal de Data Link (UDL) usando o Microsoft Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744781"
---
# <a name="universal-data-link-udl-configuration"></a>Configuração de Universal Data Link (UDL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Guia Conexão
Use a guia Conexão para especificar como conectar-se aos seus dados usando o Driver OLE DB da Microsoft para SQL Server.

![Captura de tela de páginas de Link de dados do OLE DB - guia Conexão](../media/data-link-pages-connection-tab.png)

A guia Conexão é específica do provedor e exibe apenas as propriedades de conexão necessárias ao Microsoft OLE DB Driver para SQL Server.

|Opção|Descrição|
|---   |---        |
|Selecione ou digite um nome de servidor|selecione um nome de servidor na lista suspensa ou digite o local do servidor em que o banco de dados que você deseja acessar está localizado. Selecionar o banco de dados no servidor é uma ação separada. Atualize a lista clicando em "Atualizar".
|Insira informações para entrar no servidor|Você pode selecionar as seguintes opções de autenticação da lista suspensa: <ul><li>`Windows Authentication:` Autenticação do SQL Server usando as credenciais de conta do Windows do usuário conectado no momento.</li><li>`SQL Server Authentication:` Autenticação do SQL Server usando ID de logon e senha.</li><li>`Active Directory - Integrated:` Autenticação integrada usando credenciais de conta do Windows do usuário conectado no momento.</li><li>`Active Directory - Password:` Autenticação do Active Directory usando a ID de logon e senha.</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|Nome de usuário|Digite a ID de usuário a ser usado para autenticação quando você entrar para a fonte de dados.|
|Senha|Digite a senha a ser usada para autenticação quando você entrar para a fonte de dados.|
|Senha em branco|Quando marcada, permite que o provedor especificado usar uma senha em branco na cadeia de conexão.|
|Permitir Salvamento de Senha|Quando marcada, permite que a senha a ser salva com a cadeia de caracteres de conexão. Se a senha será incluída na cadeia de conexão dependerá da funcionalidade do aplicativo de chamada. <br/><br/>**OBSERVAÇÃO:** se salva, a senha é retornada e salva sem-máscara e sem-criptografia.|
|Usar criptografia forte para dados|Quando marcada, os dados que são passados por meio de conexão serão criptografados.|
|Confiar em certificado do servidor|Quando marcada, o certificado do servidor será validado. Certificado do servidor deve ter o nome de host correto do servidor e emitido por uma autoridade de certificação confiável.|
|Selecionar o banco de dados|Selecione ou digite o nome do banco de dados que você deseja acessar.|
|Anexar arquivo de BD como nome de banco de dados|Especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e usado como o banco de dados padrão da fonte de dados. Na primeira caixa de texto nesta seção, digite o nome de banco de dados a ser usado para o arquivo de banco de dados anexado.<br/><br/>Digite o caminho completo para o arquivo de banco de dados a ser anexado na caixa de texto rotulada `Using the filename`, ou clique no `...` botão para procurar o arquivo de banco de dados.|
|Alterar Senha|Exibe a caixa de diálogo Alterar senha do SQL Server. |
|Testar Conexão|Clique para tentar uma conexão à fonte de dados especificado. Se a conexão falhar, verifique se as configurações estão corretas. Por exemplo, erros ortográficos e diferenciação de maiúsculas e minúsculas podem causar falhas de conexão.|

## <a name="advanced-tab"></a>Guia Avançado
Use a guia Avançado para exibir e definir propriedades de inicialização adicionais.

![Captura de tela de páginas de Link de dados do OLE DB - guia Avançado](../media/data-link-pages-advanced-tab.png)

|Opção|Descrição|
|---   |---        |
| Tempo limite de conexão | Especifica a quantidade de tempo (em segundos) que o Driver Microsoft OLE DB para SQL Server aguarda a conclusão da inicialização. Se o tempo limite da inicialização for alcançado, um erro será retornado e a conexão não será criada.|


> [!NOTE]  
>  Para obter mais informações de conexão de Link de dados, consulte o [visão geral da API de Link de dados](https://go.microsoft.com/fwlink/?linkid=2067432).

## <a name="next-steps"></a>Próximas etapas
- [Autentique no Azure Active Directory](../features/using-azure-active-directory.md) usando o driver do OLE DB.

- [Solicitar ao usuário as credenciais de autenticação](../help-topics/sql-server-login-dialog.md) usando o driver do OLE DB.