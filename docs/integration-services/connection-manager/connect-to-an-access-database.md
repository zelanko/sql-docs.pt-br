---
title: Conectar-se a um banco de dados Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d82334ca4c5b5efb1d956c8d3a8afe901fc94f83
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-an-access-database"></a>Conectar-se a um banco de dados do Access
  Para conectar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a uma fonte de dados do Microsoft Office Access, um gerenciador de conexões OLE DB e um provedor de dados são necessários. O provedor de dados usado depende da versão do Access que criou a fonte de dados:  
  
-   Para o Access 2003 e anterior, o pacote requer o provedor OLE DB do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet.  
  
-   Para o Access 2007, o pacote requer o provedor OLE DB para o Microsoft Office 12.0 Access Database Engine.  
  
 Você pode criar um gerenciador de conexões OLE DB e selecionar o provedor de dados correspondente na área Gerenciadores de Conexões do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou no Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access no modo de 32 bits. O provedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet e o provedor OLE DB para Mecanismo de Banco de Dados do Microsoft Office 12.0 Access estão disponíveis somente em versões de 32 bits.  

## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividade para arquivos do Microsoft Excel e Access
  
Talvez seja preciso baixar os componentes de conectividade para arquivos do Microsoft Office se eles ainda não estiverem instalados. Baixe a versão mais recente dos componentes de conectividade para arquivos do Excel e do Access aqui: [Mecanismo de Banco de Dados do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes podem abrir arquivos criados em versões anteriores do Access.

Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos componentes e precisará também certificar-se de executar o pacote no modo de 32 bits.

Se você tem uma assinatura do Office 365, verifique se você baixou o Mecanismo de Banco de Dados do Access 2016 Redistribuível e não o Tempo de Execução do Microsoft Access 2016. Quando você executar o instalador, você verá uma mensagem de erro dizendo que você não pode instalar o download lado a lado com componentes do tipo clique para executar do Office. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de Comando e executando o arquivo .EXE baixado com a opção `/quiet`. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>Conectando-se a uma fonte de dados em formato Access 2003 ou anterior  
  
### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>Para criar um gerenciador de conexão do Access na área Gerenciadores de Conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote.  
  
2.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse em qualquer lugar da área e selecione **Nova Conexão OLE DB**.  
  
3.  Na caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , clique em **Novo**.  
  
     Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  Na caixa de diálogo **Gerenciador de Conexões** , para **Provedor**, selecione **Microsoft Jet 4.0 OLE DB Provider**e configure o gerenciador de conexões conforme adequado.  
  
### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>Para criar uma conexão do Access a partir do Assistente de Importação e Exportação do SQL Server  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], inicie o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Na página **Escolher uma Fonte de Dados** , para **Fonte de dados**, selecione **Microsoft Access**e, em seguida, configure a conexão do Access.  
  
     Ao selecionar **Microsoft Access** como a **Fonte de Dados**, o assistente cria automaticamente o gerenciador de conexões OLE DB necessário com o provedor de dados correto. Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>Conectando-se a uma fonte de dados em formato Access 2007  
 Para acessar uma fonte de dados do Access 2007, o gerenciador de conexões OLE DB requer o provedor OLE DB para o Microsoft Office 12.0 Access Database Engine. Esse provedor é instalado automaticamente com o sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007. Se o sistema Office 2007 não estiver instalado no computador em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está em execução, será necessário instalar o provedor separadamente. Para instalar o provedor OLE DB para o Mecanismo de Banco de Dados do Microsoft Office 12.0 Access, faça download e instale os componentes nesta página da Web, [Driver do sistema Office 2007: Componentes de conectividade de dados](http://go.microsoft.com/fwlink/?LinkId=98155).  
  
### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>Para criar um gerenciador de conexões OLE DB na área Gerenciadores de Conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote.  
  
2.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse em qualquer lugar da área e selecione **Nova Conexão OLE DB**.  
  
3.  Na caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , clique em **Novo**.  
  
     Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  Na caixa de diálogo **Gerenciador de Conexões** , para **Provedor**, selecione **Microsoft Office 12.0 Access Database Engine OLE DB**e configure o gerenciador de conexões conforme adequado.  
  
    > [!NOTE]  
    >  Para se conectar a uma fonte de dados que usa o Access 2007, não é possível selecionar **Provedor OLE DB para Microsoft Jet 4.0** como a **Fonte de Dados**.  
  
### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>Para criar uma conexão OLE DB a partir do Assistente de Importação e Exportação do SQL Server  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], inicie o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Na página **Escolher uma Fonte de Dados** , para **Fonte de Dados**, selecione **Microsoft Office 12.0 Access Database Engine OLE DB Provider**e configure a conexão conforme adequado.  
  
    > [!NOTE]  
    >  Para se conectar a uma fonte de dados que usa o Access 2007, não é possível selecionar **Provedor OLE DB para Microsoft Jet 4.0** como a **Fonte de Dados**.  
  
     Ao selecionar **Microsoft Office 12.0 Access Database Engine OLE DB Provider** como a **Fonte de Dados**, o assistente cria automaticamente o gerenciador de conexões OLE DB necessário com o provedor de dados correto. Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
