---
title: Configuração do UDL (Universal Data Link) | Microsoft Docs
description: Saiba como usar a guia Conexão para especificar como se conectar aos seus dados usando o Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: f8d9444864dfe144918374c6d10e1a9f403faff3
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504707"
---
# <a name="universal-data-link-udl-configuration"></a>Configuração do UDL (Universal Data Link)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>Guia Conexão
Use a guia Conexão para especificar como se conectar aos seus dados usando o Driver do Microsoft OLE DB para SQL Server.

![Captura de tela das páginas de link de dados do OLE DB – guia Conexão](../media/data-link-pages-connection-tab.png)

A guia Conexão é específica do provedor e exibe apenas as propriedades de conexão necessárias ao Microsoft OLE DB Driver para SQL Server.

|Opção|DESCRIÇÃO|
|---   |---        |
|Selecione ou digite um nome de servidor|selecione um nome de servidor na lista suspensa ou digite o local do servidor em que o banco de dados que você deseja acessar está localizado. Selecionar o banco de dados no servidor é uma ação separada. Atualize a lista clicando em "Atualizar".
|Digite as informações para entrar no servidor|Você pode selecionar as seguintes opções de autenticação nesta lista suspensa: <ul><li>Autenticação do `Windows Authentication:` para SQL Server usando as credenciais da conta do Windows do usuário conectado no momento.</li><li>Autenticação do `SQL Server Authentication:` usando a ID de logon e a senha.</li><li>Autenticação integrada do `Active Directory - Integrated:` com uma identidade do Azure Active Directory. Esse modo também pode ser usado para a autenticação do Windows para SQL Server.</li><li>Autenticação de ID de usuário e senha do `Active Directory - Password:` com uma identidade do Azure Active Directory.</li><li>Autenticação interativa do `Active Directory - Universal with MFA support:` com uma identidade do Azure Active Directory. Este modo é compatível com a Autenticação Multifator (MFA) do Azure.</li><li>`Active Directory - Service Principal:` Autenticação com uma entidade de serviço do Azure Active Directory. **Nome de usuário** deve ser definido como a ID do aplicativo (cliente). **Senha** deve ser definida como o segredo do aplicativo (cliente).</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|Nome de usuário|Digite a ID de usuário a ser usada para autenticação quando você entrar na fonte de dados.|
|Senha|Digite a senha a ser usada para autenticação quando você entrar na fonte de dados.|
|Senha em branco|Quando marcada, habilita o provedor especificado a usar uma senha em branco na cadeia de conexão.|
|Permitir Salvamento de Senha|Quando marcada, permite que a senha seja salva com a cadeia de conexão. Se a senha será incluída na cadeia de conexão dependerá da funcionalidade do aplicativo de chamada. <br/><br/>**OBSERVAÇÃO:** se salva, a senha é retornada e salva sem-máscara e sem-criptografia.|
|Usar criptografia forte para dados|Quando for selecionado, os dados transmitidos pela conexão serão criptografados.|
|Confiar em certificado do servidor|Quando for selecionado, o certificado do servidor será validado. O certificado do servidor deve ter o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.|
|Selecione o banco de dados|Selecione ou digite o nome do banco de dados que você deseja acessar.|
|Anexar arquivo de BD como nome de banco de dados|Especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e usado como o banco de dados padrão da fonte de dados. Na primeira caixa de texto sob esta seção, digite o nome do banco de dados a ser usado para o arquivo de banco de dados anexado.<br/><br/>Digite o caminho completo até o arquivo de banco de dados a ser anexado na caixa de texto rotulada como `Using the filename` ou clique no botão `...` para procurar o arquivo de banco de dados.|
|Alterar Senha|Exibe a caixa de diálogo Alterar Senha do SQL Server. |
|Teste a conexão|Clique para testar uma conexão com a fonte de dados especificada. Se a conexão falhar, verifique se as configurações estão corretas. Por exemplo, erros ortográficos e diferenciação de maiúsculas e minúsculas podem causar falhas de conexão.|

## <a name="advanced-tab"></a>Guia Avançado
Use a guia Avançado para ver e definir propriedades de inicialização adicionais.

![Captura de tela das páginas de link de dados do OLE DB – guia Avançado](../media/data-link-pages-advanced-tab.png)

|Opção|DESCRIÇÃO|
|---   |---        |
| Tempo limite de conexão | Especifica a quantidade de tempo (em segundos) que o Driver do Microsoft OLE DB para SQL Server aguarda a conclusão da inicialização. Se o tempo limite da inicialização for alcançado, um erro será retornado e a conexão não será criada.|


> [!NOTE]  
>  Para obter informações gerais de conexão do vínculo de dados, confira a [Visão geral da API do Data Link](/previous-versions/windows/desktop/ms718102(v=vs.85)).

## <a name="next-steps"></a>Próximas etapas
- [Autenticar para o Azure Active Directory](../features/using-azure-active-directory.md) usando o driver do OLE DB.

- [Solicite credenciais de autenticação ao usuário](../help-topics/sql-server-login-dialog.md) usando o driver do OLE DB.