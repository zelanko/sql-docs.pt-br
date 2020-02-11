---
title: Gerenciador de conexões OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00d28ef5dbe2c0a19e5a464981934f2a84df7a7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833723"
---
# <a name="ole-db-connection-manager"></a>gerenciador de conexões OLE DB
  Um gerenciador de conexões OLE DB permite que um pacote se conecte a uma fonte de dados usando um provedor OLE DB. Por exemplo, um gerenciador de conexões OLE DB que se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar o provedor OLE DB da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]
>  O provedor de OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 não dá suporte às novas palavras-chave de cadeia de conexão (MultiSubnetFailover=True) para clustering de failover de várias sub-redes. Para obter mais informações, consulte as [notas de versão SQL Server](https://go.microsoft.com/fwlink/?LinkId=247824) e a postagem do blog, [failover de várias sub-redes AlwaysOn e SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/), em www.mattmasson.com.  
  
 Várias tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e componentes de fluxo de dados usam um gerenciador de conexões OLE DB. Por exemplo, a fonte e o destino do OLE DB usam esse gerenciador de conexões para extrair e carregar dados e a tarefa Executar SQL pode usar esse gerenciador de conexões para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar consultas.  
  
 O gerenciador de conexões OLE DB também é usado para acessar fontes de dados OLE DB em tarefas personalizadas gravadas em código não gerenciado que usa uma linguagem como C++.  
  
 Quando você adiciona um gerenciador de conexões OLE DB a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que resolverá uma conexão OLE DB em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção do `Connections` no pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `OLEDB`.  
  
 O gerenciador de conexões OLE DB pode ser configurado das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.  
  
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.  
  
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
## <a name="logging"></a>Registro em log  
 Você pode registrar as chamadas que o gerenciador de conexões OLE DB faz aos provedores de dados externos. É possível usar esse recurso de registro para solucionar problemas de conexões que o gerenciador de conexões OLE DB cria para as fontes de dados externas. Para registrar as chamadas que o Gerenciador de conexões do OLE DB faz aos provedores de dados externos, habilite o log de pacote e selecione o evento de **diagnóstico** no nível do pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuration-of-the-oledb-connection-manager"></a>Configuração do gerenciador de conexões OLEDB  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Configurar Gerenciador de Conexões OLE DB](../configure-ole-db-connection-manager.md). Para obter mais informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** no Guia do Desenvolvedor.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo do Wiki, [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (SSIS com Conectores Oracle) em social.technet.microsoft.com.  
  
-   Artigo técnico, [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Cadeias de conexão para provedores de OLE DB), em carlprothman.net.  
  
## <a name="see-also"></a>Consulte Também  
 [Origem de OLE DB](../data-flow/ole-db-source.md)   
 [Destino OLE DB](../data-flow/ole-db-destination.md)   
 [Tarefa Executar SQL](../control-flow/execute-sql-task.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
