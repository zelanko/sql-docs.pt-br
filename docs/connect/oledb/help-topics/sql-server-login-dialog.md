---
title: Caixa de diálogo de logon do SQL Server (OLE DB) | Microsoft Docs
description: Como usar a caixa de diálogo de logon do SQL Server
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 4735ead33dc7c3a6d633e3b23ff1da97eeae4962
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744789"
---
# <a name="sql-server-login-dialog-box"></a>Caixa de diálogo de logon do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Quando você tenta se conectar sem especificar informações suficientes, o driver do OLE DB exibe a **logon do SQL Server** caixa de diálogo.

> [!NOTE]  
> Diálogo de logon do SQL Server solicitando que o comportamento é controlado pelo `DBPROP_INIT_PROMPT` propriedade de inicialização. Para obter mais informações, consulte:
> - [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [Guia do programador do OLE DB](https://go.microsoft.com/fwlink/?linkid=2067702)

![Captura de tela da caixa de diálogo de logon do SQL Server](../media/sql-server-login-dialog.png)

## <a name="options"></a>Opções
|Opção|Descrição|
|---   |---        |
|Servidor|O nome de uma instância do SQL Server em sua rede. Selecione um nome de servidor\instância na lista ou digite o nome do servidor\instância na caixa **Servidor**. Se desejar, crie um alias de servidor no computador cliente usando o **SQL Server Configuration Manager** e digite esse nome na caixa **Servidor**. <br/><br/>Digite "(local)" quando estiver usando o mesmo computador como SQL Server. Assim, você pode se conectar a uma instância local do SQL Server, até mesmo ao executar uma versão não em rede do SQL Server.<br/><br/>Para obter mais informações sobre nomes de servidor para tipos diferentes de redes, consulte [instalação do SQL Server](https://go.microsoft.com/fwlink/?linkid=2067541).|
|Modo de Autenticação|Você pode selecionar as seguintes opções de autenticação na lista suspensa:<br/><ul><li>`Windows Authentication:` Autenticação do SQL Server usando as credenciais de conta do Windows do usuário conectado no momento.</li><li>`SQL Server Authentication:` Autenticação do SQL Server usando ID de logon e senha.</li><li>`Active Directory - Integrated:` Autenticação integrada usando credenciais de conta do Windows do usuário conectado no momento.</li><li>`Active Directory - Password:` Autenticação do Active Directory usando a ID de logon e senha.</li></ul>|
|SPN do servidor|Se você usar uma conexão confiável, poderá especificar um SPN (nome de entidade de serviço) para o servidor.|
|ID de Logon|Especifica a ID de logon a ser usado para a conexão. A caixa de texto de ID de logon é habilitada somente se `Authentication Mode` é definido como `SQL Server Authentication` ou `Active Directory - Password`.|
|Senha|Especifica a senha usada para a conexão. A caixa de texto de senha é habilitada somente se `Authentication Mode` é definido como `SQL Server Authentication` ou `Active Directory - Password`.|
|Opções|Exibe ou oculta o grupo **Opções**. O botão **Opções** será habilitado se **Servidor** tiver um valor.|
|Alterar Senha|Quando marcada, permite **nova senha** e **Confirmar nova senha** caixas de texto.|
|Nova Senha|Especifica a nova senha.|
|Confirmar Nova Senha|Especifica a nova senha uma segunda vez, para confirmação.|
|banco de dados|Selecione ou digite o banco de dados padrão a ser usado na conexão. Essa configuração substitui o banco de dados padrão especificado para o logon no servidor. Se nenhum banco de dados for especificado, a conexão usará o banco de dados padrão especificado para o logon no servidor.|
|Servidor Espelho|Especifica o nome do parceiro de failover do banco de dados a ser espelhado.|
|SPN do espelho|Se desejar, especifique um SPN para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.|
|Linguagem|Especifica o idioma nacional a ser usado para mensagens de sistema do SQL Server. O computador que executa o SQL Server deve ter o idioma instalado. Essa configuração substitui o idioma padrão especificado para o logon no servidor. Se nenhum idioma for especificado, a conexão usará o idioma padrão especificado para o logon no servidor.|
|Nome do Aplicativo|Especifica o nome do aplicativo a ser armazenado na coluna **program_name** na linha dessa conexão em **sys.sysprocesses**.|
|ID da Estação de Trabalho|Especifica a ID da estação de trabalho a ser armazenada na coluna **hostname** na linha dessa conexão em **sys.sysprocesses**.|
|Usar criptografia forte para dados|Quando marcada, os dados que são passados por meio de conexão serão criptografados.|
|Confiar em certificado do servidor|Quando marcada, o certificado do servidor será validado. Certificado do servidor deve ter o nome de host correto do servidor e emitido por uma autoridade de certificação confiável.|

> [!NOTE]  
> Ao usar `Windows Authentication` ou `SQL Server Authentication` modos de **certificado do servidor confiável** é considerado somente quando o **usar criptografia forte para dados** opção está habilitada.

## <a name="next-steps"></a>Próximas etapas
- [Autentique no Azure Active Directory](../features/using-azure-active-directory.md) usando o driver do OLE DB.
- Informações de conexão de conjunto usando [Universal Data Link (UDL)](data-link-pages.md).