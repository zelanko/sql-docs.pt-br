---
title: Gerenciador de conexões OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ee9368848e7c939bbc8d4bb14eb49014ef5efb48
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728169"
---
# <a name="ole-db-connection-manager"></a>gerenciador de conexões OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um gerenciador de conexões OLE DB permite que um pacote se conecte a uma fonte de dados usando um provedor OLE DB. Por exemplo, um gerenciador de conexões OLE DB que se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar o provedor OLE DB da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  O provedor de OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 não dá suporte às novas palavras-chave de cadeia de conexão (MultiSubnetFailover=True) para clustering de failover de várias sub-redes. Para obter mais informações, consulte as [SQL Server Release Notes](https://go.microsoft.com/fwlink/?LinkId=247824) (Notas de versão do SQL Server) e o post do blog [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)(Failover de várias sub-redes AlwaysOn e SSIS) em www.mattmasson.com.    
> 
> [!NOTE]
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor de dados diferente das versões anteriores do Excel ou do Access. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) e [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 Várias tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e componentes de fluxo de dados usam um gerenciador de conexões OLE DB. Por exemplo, a fonte e o destino do OLE DB usam esse gerenciador de conexões para extrair e carregar dados e a tarefa Executar SQL pode usar esse gerenciador de conexões para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar consultas.    
    
 O gerenciador de conexões OLE DB também é usado para acessar fontes de dados OLE DB em tarefas personalizadas gravadas em código não gerenciado que usa uma linguagem como C++.    
    
 Ao adicionar um gerenciador de conexões OLE DB a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do OLE DB em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote.    
    
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **OLEDB**.    
    
 O gerenciador de conexões OLE DB pode ser configurado das seguintes maneiras:    
    
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.    
    
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.    
    
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.    
    
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.    
    
## <a name="logging"></a>Log    
 Você pode registrar as chamadas que o gerenciador de conexões OLE DB faz aos provedores de dados externos. É possível usar esse recurso de registro para solucionar problemas de conexões que o gerenciador de conexões OLE DB cria para as fontes de dados externas. Para registrar as chamadas que o gerenciador de conexões OLE DB cria para os provedores de dados externos, habilite o registro do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Configuração do gerenciador de conexões OLEDB    
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Para obter mais informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** no Guia do Desenvolvedor.    
    
## <a name="related-content"></a>Conteúdo relacionado    
    
-   Artigo do Wiki, [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (SSIS com Conectores Oracle) em social.technet.microsoft.com.    
    
-   Artigo técnico, [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Cadeias de conexão para provedores de OLE DB), em carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>Configurar Gerenciador de Conexões OLE DB
  Use a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** para adicionar uma conexão a uma fonte de dados, seja ela uma nova conexão ou a cópia de uma conexão existente.  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Se a fonte de dados for o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor OLE DB diferente das versões anteriores do Access. Para obter mais informações, consulte [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Para obter mais informações sobre o gerenciador de conexões OLE DB, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Conexões de dados**  
 Selecione uma conexão de dados OLE DB existente na lista.  
  
 **Propriedades de conexão de dados**  
 Exiba as propriedades e os valores da conexão de dados OLE DB selecionada.  
  
 **Nova**  
 Crie uma conexão de dados OLE DB usando a caixa de diálogo **Gerenciador de Conexões** .  
  
 **Delete (excluir)**  
 Selecione uma conexão de dados e a exclua usando o botão **Excluir** .  
  
## <a name="see-also"></a>Consulte Também    
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
