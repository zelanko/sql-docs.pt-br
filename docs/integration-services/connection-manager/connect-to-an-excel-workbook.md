---
title: "Conectar-se a uma pasta de trabalho do Excel | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Excel [Integration Services]"
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Conectar-se a uma pasta de trabalho do Excel
  A conexão de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a uma pasta de trabalho do Microsoft Office Excel requer um gerenciador de conexões do Excel.  
  
 Você pode criar esses gerenciadores de conexões na área Gerenciadores de Conexões do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou no Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Provedores e drivers para arquivos do Microsoft Excel e Access**  
  
 Você precisará baixar os provedores OLE DB e drivers para arquivos do Microsoft Office se eles ainda não estiverem instalados. Versões mais recentes do provedor podem abrir arquivos criados em versões anteriores do Excel.  
  
 Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos drivers e precisará também certificar-se de executar o assistente ou o pacote do Integration Services que ele cria no modo de 32 bits.  
  
|Versão do Microsoft Office|Download|  
|------------------------------|--------------|  
|2007|[2007 Office System Driver: componentes de conectividade de dados](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Tempo de execução do Microsoft Access 2010](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Tempo de execução do Microsoft Access 2013](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
### Para criar um gerenciador de conexões do Excel na área Gerenciadores de Conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote.  
  
2.  Na área **Gerenciadores de Conexões**, clique com o botão direito do mouse em qualquer lugar da área e, em seguida, selecione **Nova Conexão**.  
  
3.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS**, selecione **Excel** e configure o gerenciador de conexões.  
  
     Para obter informações sobre as opções de configuração que estão disponíveis para este gerenciador de conexões, consulte [Editor de Gerenciador de Conexões Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### Para criar uma conexão do Excel a partir do Assistente de Importação e Exportação do SQL Server  
  
1.  Inicie a versão de 32 bits do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Na página **Escolher uma Fonte de Dados**, para **Fonte de Dados**, selecione **Microsoft Excel** e configure a conexão do Excel.  
  
     Para obter informações sobre as opções de configuração que estão disponíveis para este tipo de conexão, consulte [Editor de Gerenciador de Conexões Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## Consulte também  
 [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  