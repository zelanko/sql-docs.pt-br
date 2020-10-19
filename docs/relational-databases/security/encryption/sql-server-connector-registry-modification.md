---
title: Registro em log de informações e erros do Conector do SQL Server
description: Este artigo descreve como habilitar registro em log e erros do Conector do SQL Server modificando as entradas do Registro
ms.date: 10/08/2020
ms.localizationpriority: medium
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: how-to
author: rupp29
ms.author: arupp
ms.openlocfilehash: 85be425e0e352961841f5317c7db219153a6c008
ms.sourcegitcommit: 9122251ab8bbd46ea3c699e741d6842c995195fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91847727"
---
# <a name="sql-server-connector-error-and-information-logging"></a>Registro em log de informações e erros do Conector do SQL Server

Este artigo descreve a modificação de entradas do Registro para habilitar registro em log de informações e erros do Conector do SQL Server.

## <a name="sql-server-connector-for-microsoft-azure-key-vault"></a>Conector do SQL Server para Cofre de Chaves do Microsoft Azure

O [Conector do SQL Server para Microsoft Azure Key Vault](https://www.microsoft.com/download/details.aspx?id=45344) permite que a criptografia do SQL Server use o Microsoft Azure Key Vault como um provedor EKM (gerenciamento extensível de chaves) para proteger as chaves de criptografia.

O [download](https://www.microsoft.com/download/details.aspx?id=45344) consiste no Conector do SQL Server e scripts de exemplo que permitem que um Administrador do SQL Server saiba como configurar o Conector do SQL Server e habilitar cenários de criptografia do SQL Server. Para obter mais informações, confira [Gerenciamento extensível de chaves usando o Key Vault (SQL Server)](https://go.microsoft.com/fwlink/p/?LinkId=521690).

Use o [fórum do Azure Key Vault](https://social.msdn.microsoft.com/Forums/AzureKeyVault) para fazer perguntas, compartilhar insights e discutir o Conector do SQL Server.

> [!NOTE]
> Durante a execução normal, o DLL do Conector do SQL Server criará entradas de Registro dinamicamente para estabelecer a conectividade com o Azure Key Vault, a fim de criar a Chave `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQL Server Cryptographic Provider]`. A conta de inicialização do SQL Server precisa ser um administrador local ou a conta de serviço dela precisa ser **NT SERVICE\MSSQLSERVER**

## <a name="upgrade-sql-server-connector-to-the-latest-version"></a>Atualizar o Conector do SQL Server para a versão mais recente

Para atualizar o Conector do SQL Server (Versão: 1.0.5.0 com uma data de setembro de 2020) para a versão mais recente do provedor de Criptografia DLL, siga estas etapas.

### <a name="upgrade"></a>Atualizar

1. Interrompa o serviço SQL Server usando o SQL Server Configuration Manager
1. Desinstale a versão antiga usando **Painel de Controle\Programas\Programas e Recursos**
    1. Nome do aplicativo: Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.300.96
    1. Data do arquivo DLL: 30/01/2018 15:00
1. Instalar (atualizar) o novo Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.2000.367
    1. Data do arquivo DLL: 11/09/2020 ‏‎5:17
1. Iniciar o serviço SQL Server
1. Os BDs criptografados de teste estão acessíveis

### <a name="rollback"></a>Reversão

1. Interrompa o serviço SQL Server usando o SQL Server Configuration Manager
1. Desinstale a nova versão usando **Painel de Controle\Programas\Programas e Recursos**
    1. Nome do aplicativo: Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.2000.367
    1. Data do arquivo DLL: 11/09/2020 ‏‎5:17
1. Instalar a versão antiga do Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.300.96
    1. Data do arquivo DLL: 30/01/2018 15:00
1. Iniciar o serviço SQL Server
1. Os BDs criptografados de teste estão acessíveis

> [!NOTE]
> - As versões 1.0.0.440 e anteriores do Conector do SQL Server foram substituídas e não têm mais suporte em ambientes de produção. Para obter mais informações sobre como solucionar problemas do Conector do SQL Server, confira [Solução de problemas e manutenção do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).
> - Da versão 1.0.3.0 em diante, o Conector do SQL Server relata mensagens de erro relevantes para os logs de eventos do Windows para solução de problemas.
> - Da versão [1.0.4.0: (versão 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi) em diante, há suporte para nuvens privadas do Azure, incluindo o Azure China, o Azure Alemanha e o Azure Government.
> - Há uma alteração da falha na versão 1.0.5.0, em termos do algoritmo de impressão digital. Você pode enfrentar falhas de restauração do banco de dados após atualizar para a 1.0.5.0. Para saber mais, confira o [artigo da base de dados de conhecimento 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0).
> - **Da versão 1.0.5.0 em diante (com uma data de arquivo de setembro de 2020), o Conector do SQL Server dá suporte à filtragem de mensagens e lógica de repetição de solicitação de rede.**
> - *A versão antiga do Conector do SQL Server também é a versão: [1.0.5.0 (versão 15.0.300.96) – Data do arquivo de janeiro de 2018](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)* . Atualize para a Conector do SQL Server mais recente se você tiver problemas.

**Requisitos do sistema** – Versões do SQL Server com suporte:

- SQL Server 2019 RTM Enterprise (64 bits)
- SQL Server 2017 RTM Enterprise (64 bits)
- SQL Server 2016 RTM Enterprise (64 bits)
- SQL Server 2014 RTM Enterprise (64 bits)
- SQL Server 2012 SP2 Enterprise (64 bits)
- SQL Server 2012 SP1 CU6 Enterprise (64 bits)
- SQL Server 2008 R2 SP2 CU8 Enterprise (64 bits)

Nas versões do SQL Server 2008 e 2012 inferiores àquelas listadas acima, o patch especificado no seguinte artigo da base de dados precisa ser instalado: [https://support2.microsoft.com/kb/2859713](https://support2.microsoft.com/kb/2859713).

O Conector do SQL Server para Microsoft Azure Key Vault também requer o .NET Versão 4.5.1 na Máquina Virtual do Microsoft SQL Server no Azure. Essa biblioteca deve ser instalada antes de você instalar o Conector do SQL Server.

Instale a versão apropriada do Pacote Redistribuível do Visual Studio C++ com base na versão do SQL Server que está sendo executada:

- Para o SQL Server versões 2008, 2008 R2, 2012 e 2014, instale o 2013 Pacote Redistribuível do Visual C++.

- Para o SQL Server 2016, instale o 2015 Pacote Redistribuível do Visual C++.

## <a name="modify-windows-registry-steps"></a>Etapas para modificar o Registro do Windows

Modifique as entradas do Registro para habilitar que o Conector do SQL Server registre em log eventos de informações e erros no Log de Eventos do Aplicativo do Windows.

> [!CAUTION]
> Siga as etapas nesta seção com cuidado e por sua conta e risco. Poderão ocorrer problemas graves se você modificar o Registro incorretamente. Antes de modificar o Registro, [faça backup do Registro para restauração](https://support.microsoft.com/help/322756), caso ocorram problemas.

1. Há duas maneiras de abrir o Editor do Registro no Windows 10:
    - Na caixa de pesquisa na barra de tarefas, digite **regedit**. Em seguida, selecione o resultado principal do Editor do Registro (aplicativo da área de trabalho).

    ![ekm regedit open](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-open.png "ekm regedit open")
    - Pressione e segure ou clique com o botão direito do mouse no botão Iniciar e selecione Executar. Insira **regedit** na caixa de diálogo e selecione **OK**.

   ![ekm regedit start](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-start.png "ekm regedit start")

1. Navegue até esta chave do Registro:

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\**

    ![ekm regedit akv](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv.png "ekm regedit akv")  

1. Adicione uma nova Chave em **Azure Key Vault** chamada `Log`:

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log.png "ekm regedit akv log.png")  

1. Abaixo da chave **Log**, adicione um valor DWORD (32 bits) chamado `Level`:

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log dword](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-dword.png "ekm regedit akv log dword")  

1. Defina o valor do DWORD como um Nível de Log apropriado (0,1,2):
   1. 0 (Informações) – **Padrão**
   1. 1 (Erro)
   1. 2 (Sem Log)

   ![ekm regedit akv log level](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-level.png "ekm regedit akv log level")  

As entradas do Registro descritas neste artigo são encontradas sob esta chave:

```console
\Computer
    \HKEY_LOCAL_MACHINE
       \SOFTWARE
          \Microsoft
             \SQL Server Cryptographic Provider
                \Azure Key Vault
                   \Log\
                      <Level>
```

Opcionalmente, você pode usar a linha de comando para gerar a chave:

```cmd
--Create the logging parameter using (Administrator) Command Line:
REG ADD "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level /t REG_DWORD /d 1 

--Validate the new registry entry
REG QUERY "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level
```

As entradas do log de eventos do aplicativo que têm mensagens ausentes também podem ser consertadas usando uma entrada de Registro. O log de eventos pode conter a mensagem `The description for Event ID 0 from source SQL Server Connector for Microsoft Azure Key Vault cannot be found...`.  

```cmd
--Create the registry entry to enable missing messages (this works with any version)
REG ADD "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile /t REG_EXPAND_SZ /d "C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll"

--Validate the new registry entry
REG QUERY "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile
```

## <a name="related-articles"></a>Artigos relacionados

- Para ver mais scripts de exemplo, confira o blog em [Transparent Data Encryption e Gerenciamento Extensível de Chaves do SQL Server com o Azure Key Vault](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)
- [EKM (Gerenciamento extensível de chaves)](extensible-key-management-ekm.md)  
- [Gerenciamento Extensível de Chaves com o Azure Key Vault](extensible-key-management-using-azure-key-vault-sql-server.md)
- [Manutenção e solução de problemas do conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
