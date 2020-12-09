---
title: Caixa de diálogo Logon do SQL Server (OLE DB) | Microsoft Docs
description: Quando você tenta se conectar sem especificar informações o suficiente, o Driver do OLE DB para SQL Server exibe a caixa de diálogo de Logon do SQL Server.
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 97b52f8c1e4560c5fe1654d8e81d2ac00cdb6257
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506376"
---
# <a name="sql-server-login-dialog-box"></a>Caixa de diálogo de logon do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Quando você tenta se conectar sem especificar informações o suficiente, o driver do OLE DB exibe a caixa de diálogo **Logon do SQL Server**.

> [!NOTE]  
> O comportamento de solicitação da Caixa de Diálogo do SQL Server é controlado pela propriedade de inicialização do `DBPROP_INIT_PROMPT`. Para obter mais informações, consulte:
> - [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guia do Programador do OLE DB](/previous-versions/windows/desktop/ms714342(v=vs.85))

![Captura de tela da Caixa de Diálogo de Logon do SQL Server](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opções
|Opção|Descrição|
|---   |---        |
|Servidor|O nome de uma instância do SQL Server na sua rede. Selecione um nome de servidor\instância na lista ou digite o nome do servidor\instância na caixa **Servidor**. Se desejar, crie um alias de servidor no computador cliente usando o **SQL Server Configuration Manager** e digite esse nome na caixa **Servidor**. <br/><br/>Digite "(local)" quando estiver usando o mesmo computador como SQL Server. Assim, você pode se conectar a uma instância local do SQL Server, até mesmo ao executar uma versão não em rede do SQL Server.<br/><br/>Para obter mais informações sobre nomes de servidor para diferentes tipos de rede, confira [Instalação do SQL Server](../../../database-engine/install-windows/install-sql-server.md).|
|Modo de autenticação|Você pode selecionar as seguintes opções de autenticação na lista suspensa:<br/><ul><li>Autenticação do `Windows Authentication:` para SQL Server usando as credenciais da conta do Windows do usuário conectado no momento.</li><li>Autenticação do `SQL Server Authentication:` usando a ID de logon e a senha.</li><li>Autenticação integrada do `Active Directory - Integrated:` com uma identidade do Azure Active Directory. Esse modo também pode ser usado para a autenticação do Windows para SQL Server.</li><li>Autenticação de ID de usuário e senha do `Active Directory - Password:` com uma identidade do Azure Active Directory.</li><li>Autenticação interativa do `Active Directory - Universal with MFA support:` com uma identidade do Azure Active Directory. Este modo é compatível com a Autenticação Multifator (MFA) do Azure.</li><li>`Active Directory - Service Principal:` autenticação com uma entidade de serviço do Azure Active Directory. **ID de logon** deve ser definida como a ID do aplicativo (cliente). **Senha** deve ser definida como o segredo do aplicativo (cliente).</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|ID de Logon|Especifica a ID de logon a ser usada na conexão. A caixa de texto ID de logon só será habilitada se `Authentication Mode` for definido como `SQL Server Authentication`, `Active Directory - Password`, `Active Directory - Universal with MFA support` ou `Active Directory - Service Principal`.|
|Senha|Especifica a senha usada para a conexão. A caixa de texto de senha só será habilitada se `Authentication Mode` for definido como `SQL Server Authentication`, `Active Directory - Password` ou `Active Directory - Service Principal`.|
|Opções|Exibe ou oculta o grupo **Opções**. O botão **Opções** será habilitado se **Servidor** tiver um valor.|
|Alterar Senha|Quando selecionado, habilita as caixas de texto **Nova senha** e **Confirmar nova senha**.|
|Nova senha|Especifica a nova senha.|
|Confirmar Nova Senha|Especifica a nova senha uma segunda vez, para confirmação.|
|Banco de dados|Selecione ou digite o banco de dados padrão a ser usado na conexão. Essa configuração substitui o banco de dados padrão especificado para o logon no servidor. Se nenhum banco de dados for especificado, a conexão usará o banco de dados padrão especificado para o logon no servidor.|
|Servidor Espelho|Especifica o nome do parceiro de failover do banco de dados a ser espelhado.|
|SPN do espelho|Se desejar, especifique um SPN para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.|
|Linguagem|Especifica o idioma nacional a ser usado para mensagens de sistema do SQL Server. O computador que executa o SQL Server deve ter o idioma instalado. Essa configuração substitui o idioma padrão especificado para o logon no servidor. Se nenhum idioma for especificado, a conexão usará o idioma padrão especificado para o logon no servidor.|
|Nome do Aplicativo|Especifica o nome do aplicativo a ser armazenado na coluna **program_name** na linha dessa conexão em **sys.sysprocesses**.|
|ID da Estação de Trabalho|Especifica a ID da estação de trabalho a ser armazenada na coluna **hostname** na linha dessa conexão em **sys.sysprocesses**.|
|Usar criptografia forte para dados|Quando for selecionado, os dados transmitidos pela conexão serão criptografados.|
|Confiar em certificado do servidor|Quando for selecionado, o certificado do servidor será validado. O certificado do servidor deve ter o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável.|

> [!NOTE]  
> Ao usar os modos `Windows Authentication` ou `SQL Server Authentication`, o **Certificado do servidor confiável** é considerado somente quando a opção **Usar criptografia forte para os dados** está habilitada.

## <a name="next-steps"></a>Próximas etapas
- [Autenticar para o Azure Active Directory](../features/using-azure-active-directory.md) usando o driver do OLE DB.
- Defina as informações de conexão usando o [Universal Data Link (UDL)](data-link-pages.md).