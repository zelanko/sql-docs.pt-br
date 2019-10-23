---
title: Caixa de diálogo SQL Server logon (OLE DB) | Microsoft Docs
description: Como usar a caixa de diálogo de logon do SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d35c339798b4385cb903d8a4a83f13184bbf4db3
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381752"
---
# <a name="sql-server-login-dialog-box"></a>Caixa de diálogo de logon do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Quando você tenta se conectar sem especificar informações suficientes, o driver OLE DB exibe a caixa de diálogo **SQL Server logon** .

> [!NOTE]  
> SQL Server comportamento de solicitação de diálogo de logon é controlado pela propriedade de inicialização `DBPROP_INIT_PROMPT`. Para obter mais informações, consulte:
> - [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guia do programador de OLE DB](https://go.microsoft.com/fwlink/?linkid=2067702)

![Captura de tela da caixa de diálogo SQL Server logon](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opções
|Opção|Descrição|
|---   |---        |
|Servidor|O nome de uma instância do SQL Server em sua rede. Selecione um nome de servidor\instância na lista ou digite o nome do servidor\instância na caixa **Servidor**. Se desejar, crie um alias de servidor no computador cliente usando o **SQL Server Configuration Manager** e digite esse nome na caixa **Servidor**. <br/><br/>Digite "(local)" quando estiver usando o mesmo computador como SQL Server. Assim, você pode se conectar a uma instância local do SQL Server, até mesmo ao executar uma versão não em rede do SQL Server.<br/><br/>Para obter mais informações sobre nomes de servidor para diferentes tipos de redes, consulte [SQL Server Installation](https://go.microsoft.com/fwlink/?linkid=2067541).|
|Modo de Autenticação|Você pode selecionar as seguintes opções de autenticação na lista suspensa:<br/><ul><li>`Windows Authentication:` autenticação para SQL Server usando as credenciais de conta do Windows do usuário conectado no momento.</li><li>`SQL Server Authentication:` autenticação usando a ID de logon e a senha.</li><li>`Active Directory - Integrated:` autenticação integrada com uma identidade de Azure Active Directory. Esse modo também pode ser usado para a autenticação do Windows para SQL Server.</li><li>`Active Directory - Password:` a ID de usuário e a autenticação de senha com uma identidade de Azure Active Directory.</li><li>`Active Directory - Universal with MFA support:` a autenticação interativa com uma identidade de Azure Active Directory. Esse modo dá suporte à MFA (autenticação multifator) do Azure.</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|ID de Logon|Especifica a ID de logon a ser usada para a conexão. A caixa de texto ID de logon só será habilitada se `Authentication Mode` for definida como `SQL Server Authentication`, `Active Directory - Password` ou `Active Directory - Universal with MFA support`.|
|Senha|Especifica a senha usada para a conexão. A caixa de texto senha só será habilitada se `Authentication Mode` estiver definida como `SQL Server Authentication` ou `Active Directory - Password`.|
|Opções|Exibe ou oculta o grupo **Opções**. O botão **Opções** será habilitado se **Servidor** tiver um valor.|
|Alterar Senha|Quando marcada, habilita as caixas de texto **nova senha** e **confirmar nova senha** .|
|Nova Senha|Especifica a nova senha.|
|Confirmar Nova Senha|Especifica a nova senha uma segunda vez, para confirmação.|
|banco de dados|Selecione ou digite o banco de dados padrão a ser usado na conexão. Essa configuração substitui o banco de dados padrão especificado para o logon no servidor. Se nenhum banco de dados for especificado, a conexão usará o banco de dados padrão especificado para o logon no servidor.|
|Servidor Espelho|Especifica o nome do parceiro de failover do banco de dados a ser espelhado.|
|SPN do espelho|Se desejar, especifique um SPN para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.|
|Linguagem|Especifica o idioma nacional a ser usado para mensagens de sistema do SQL Server. O computador que executa o SQL Server deve ter o idioma instalado. Essa configuração substitui o idioma padrão especificado para o logon no servidor. Se nenhum idioma for especificado, a conexão usará o idioma padrão especificado para o logon no servidor.|
|Nome do Aplicativo|Especifica o nome do aplicativo a ser armazenado na coluna **program_name** na linha dessa conexão em **sys.sysprocesses**.|
|ID da Estação de Trabalho|Especifica a ID da estação de trabalho a ser armazenada na coluna **hostname** na linha dessa conexão em **sys.sysprocesses**.|
|Usar criptografia forte para dados|Quando marcada, os dados passados pela conexão serão criptografados.|
|Confiar em certificado do servidor|Quando marcada, o certificado do servidor será validado. O certificado do servidor deve ter o nome de host correto do servidor e emitido por uma autoridade de certificação confiável.|

> [!NOTE]  
> Ao usar os modos `Windows Authentication` ou `SQL Server Authentication`, o **certificado do servidor de confiança** é considerado somente quando a opção **usar criptografia forte para dados** está habilitada.

## <a name="next-steps"></a>Próximas etapas
- [Autenticar para Azure Active Directory](../features/using-azure-active-directory.md) usando o driver OLE DB.
- Definir informações de conexão usando [Universal Data Link (udl)](data-link-pages.md).