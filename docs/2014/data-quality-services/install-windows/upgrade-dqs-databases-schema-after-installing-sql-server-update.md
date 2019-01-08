---
title: Atualizar o esquema de bancos de dados DQS depois de instalar a atualização do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d4f5af2a9b0c58e8cef89f143e4ec42cb03695
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372918"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>Atualize o esquema de bancos de dados DQS depois de instalar a atualização do SQL Server
  Depois que instalar uma atualização do SQL Server (patch, hotfix ou atualização cumulativa) em uma instância do DQS previamente configurada, você poderá ter de atualizar o esquema de bancos de dados do DQS executando o arquivo DQSInstaller.exe com o parâmetro de linha de comando **upgrade** . Caso contrário, você poderá receber o erro a seguir ao tentar se conectar ao Servidor do Data Quality usando seu Cliente do Data Quality:  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 Atualizar esquema de bancos de dados do DQS não afeta seus dados existentes nos bancos de dados do DQS (bases de dados de conhecimento, projetos de qualidade de dados e resultados exportados no banco de dados DQS_STAGING_DATA). No entanto, você deve fazer backup de seus bancos de dados do DQS antes de atualizar o esquema de bancos de dados do DQS para impedir qualquer perda de dados acidental durante a atualização do esquema. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../backing-up-and-restoring-dqs-databases.md).  
  
> [!NOTE]  
>  A maioria das atualizações do SQL Server exigirá uma atualização para o esquema de bancos de dados do DQS. Para obter informações sobre as atualizações do SQL Server que exigirão uma atualização para o esquema de bancos de dados do DQS, consulte o gráfico na etapa 1.A em [atualizar DQS: Instalando atualizações cumulativas ou Patches de Hotfix no Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve estar conectado como um membro do grupo Administradores no computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server em que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] está instalado.  
  
### <a name="to-upgrade-dqs-databases-schema"></a>Para atualizar o esquema de bancos de dados do DQS  
  
1.  (Recomendado) Faça backup de seus bancos de dados do DQS antes de continuar com a atualização de esquema. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../backing-up-and-restoring-dqs-databases.md).  
  
2.  Iniciar o prompt de comando.  
  
3.  Ao prompt de comando, altere seu diretório ao local onde DQSInstaller.exe está disponível. Se você instalou a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  No prompt de comando, digite o seguinte comando e pressione ENTER:  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  O instalador solicita que você faça backup dos bancos de dados do DQS antes de continuar. Se você já tiver feito backup dos bancos de dados do DQS, digite `Y` ou `Yes` e pressione ENTER para continuar com a atualização.  
  
6.  Uma mensagem de conclusão é exibida depois da atualização bem-sucedida do esquema de bancos de dados do DQS.  
  
## <a name="next-steps"></a>Próximas etapas  
 Faça logon no Servidor do Data Quality de um aplicativo Cliente do Data Quality.  
  
 Para obter mais informações sobre como atualizar o DQS, o esquema de bancos de dados após a instalação do SQL Server atualiza e etapas de solução de problemas associadas, consulte [atualizar DQS: Instalando atualizações cumulativas ou Patches de Hotfix no Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Data Quality Services](install-data-quality-services.md)   
 [Atualizar assemblies SQLCLR após atualizar o .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
