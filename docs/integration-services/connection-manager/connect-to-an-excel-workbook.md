---
title: Conectar-se a uma pasta de trabalho do Excel | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3c4988017daa41e12f9d640120b6841361232d1e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-an-excel-workbook"></a>Conectar-se a uma pasta de trabalho do Excel
  A conexão de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a uma pasta de trabalho do Microsoft Office Excel requer um gerenciador de conexões do Excel.  
  
 Você pode criar esses gerenciadores de conexões na área Gerenciadores de Conexões do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou no Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividade para arquivos do Microsoft Excel e Access
  
Talvez seja preciso baixar os componentes de conectividade para arquivos do Microsoft Office se eles ainda não estiverem instalados. Baixe a versão mais recente dos componentes de conectividade para arquivos do Excel e do Access aqui: [Mecanismo de Banco de Dados do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes podem abrir arquivos criados em versões anteriores do Excel.

Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos componentes e precisará também certificar-se de executar o pacote no modo de 32 bits.

Se você tem uma assinatura do Office 365, verifique se você baixou o Mecanismo de Banco de Dados do Access 2016 Redistribuível e não o Tempo de Execução do Microsoft Access 2016. Quando você executar o instalador, você verá uma mensagem de erro dizendo que você não pode instalar o download lado a lado com componentes do tipo clique para executar do Office. Para ignorar essa mensagem de erro e instalar os componentes com êxito, execute a instalação no modo silencioso abrindo uma janela de Prompt de Comando e executando o arquivo .EXE baixado com a opção `/quiet`. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Criar um gerenciador de conexões do Excel

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>Para criar um gerenciador de conexões do Excel na área Gerenciadores de Conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote.  
  
2.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse em qualquer lugar da área e, em seguida, selecione **Nova Conexão**.  
  
3.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione **Excel**e configure o gerenciador de conexões.  
  
     Para obter informações sobre as opções de configuração que estão disponíveis para este gerenciador de conexões, consulte [Editor de Gerenciador de Conexões Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>Para criar uma conexão do Excel a partir do Assistente de Importação e Exportação do SQL Server  
  
1.  Inicie a versão de 32 bits do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Na página **Escolher uma Fonte de Dados** , para **Fonte de Dados**, selecione **Microsoft Excel**e configure a conexão do Excel.  
  
     Para obter informações sobre as opções de configuração que estão disponíveis para este tipo de conexão, consulte [Editor de Gerenciador de Conexões Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
