---
title: Destino do fluxo de dados | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e95b4d887bea5783be935a40877d590b8e8dcff
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="data-streaming-destination"></a>Destino do Fluxo de Dados
  O **Destino do Fluxo de Dados** é um componente de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS), que permite que o **Provedor OLE DB para SSIS** consuma a saída de um pacote SSIS como um conjunto de resultados de tabelas. Você pode criar um servidor vinculado que use o Provedor OLE DB para SSIS e então execute uma consulta SQL no servidor vinculado para exibir os dados retornados pelo pacote SSIS.  
  
 No exemplo a seguir, a consulta a seguir retorna a saída do pacote Package.dtsx no projeto SSISPackagePublishing na pasta do Power BI do Catálogo do SSIS. Essa consulta usa o servidor vinculado chamado [Servidor Vinculado Padrão para o Integration Services] que, por sua vez, usa o novo Provedor OLE DB para SSIS. A consulta inclui o nome da pasta, o nome do projeto e o nome do pacote no catálogo do SSIS. O Provedor OLE DB para SSIS executa o pacote especificado na consulta e retorna o conjunto de resultados tabulares.  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Componentes de publicação de feed de dados  
 Os Componentes de publicação de feed de dados incluem: Provedor OLE DB para SSIS, Destino do Fluxo de Dados e o Assistente de Publicação de Pacote do SSIS. O assistente permite que você publique um pacote do SSIS como uma exibição SQL em uma instância de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O assistente ajuda você na criação de um servidor vinculado que use o Provedor OLE DB para SSIS e uma exibição SQL que representa uma consulta no servidor vinculado. Execute a exibição para consultar os resultados do pacote do SSIS como um conjunto de dados tabulares.  
  
 Para confirmar se o provedor SSISOLEDB está instalado no SQL Server Management Studio, expanda **Objetos de Servidor**, **Servidores Vinculados**, **Provedores**e confirme se o provedor **SSISOLEDB** é exibido. Clique duas vezes em **SSISOLEDB**, habilite **Permitir Inprocess** se ele não estiver habilitado e clique em **OK**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Publicar um pacote do SSIS como uma exibição SQL  
 O procedimento a seguir descreve as etapas para publicar um pacote do SSIS como uma exibição do SQL.  
  
1.  Crie um pacote do SSIS com um componente de **Destino do Fluxo de Dados** e implante o pacote no Catálogo do SSIS.  
  
2.  Execute o **Assistente de Publicação de Pacote do SSIS** executando ISDataFeedPublishingWizard.exe em C:\Arquivos de Programas\Microsoft SQL Server\130\DTS\Binn ou executando o Assistente de Publicação de Feed de Dados do menu Iniciar.  
  
     O assistente cria um servidor vinculado usando o SSISOLEDB (Provedor OLE DB para SSIS) e cria uma exibição SQL que consiste em uma consulta no servidor vinculado. Essa consulta inclui o nome da pasta, o nome do projeto e o nome do pacote no catálogo do SSIS.  
  
3.  Execute a exibição SQL no SQL Server Management Studio e verifique os resultados do pacote do SSIS. A exibição envia a consulta para o Provedor OLE DB para SSIS por meio do servidor vinculado criado por você. O Provedor OLE DB para SSIS executa o pacote especificado na consulta e retorna o conjunto de resultados tabulares.  
  
> [!IMPORTANT]  
>  Para obter etapas detalhadas, veja [Passo a passo: publicar um pacote do SSIS como uma exibição SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>Expor dados de saída de um pacote do SSIS como um feed OData usando o Centro de Administração do Power BI  
 Ao usar o Centro de Administração do Power BI, os administradores de TI podem expor dados de fontes de dados locais como feeds OData para usuários. O Centro de Administração do Power BI, por padrão, permite que você registre apenas as fontes de dados do SQL Server. No entanto, você pode registrar os pacotes do SSIS como fontes de dados com o portal usando o **Destino do Fluxo de Dados** e o **Provedor Microsoft OLE DB para SQL Server Integration Services (SSISOLEDB)** e expor os dados resultantes do pacote do SSIS como um feed OData para o usuário.  
  
 O Centro de Administração permite que você publique exibições em um banco de dados do SQL Server. Dessa forma, você pode usar o Assistente de Publicação de Pacote do SSIS para publicar um pacote do SSIS como uma exibição do SQL. Em seguida, você pode selecionar a exibição a ser incluída no feed OData no Centro de Administração do Power BI. Um administrador de dados pode consumir o feed do pacote do SSIS usando o suplemento Power Query para Excel.  
  
 Para obter instruções detalhadas, veja [Publicar pacotes do SSIS como fontes de feed OData](http://go.microsoft.com/fwlink/?LinkID=317367).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Passo a passo: publicar um pacote do SSIS como uma exibição SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [Configurar destino do fluxo de dados](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## <a name="see-also"></a>Consulte também  
 [Publicar pacotes do SSIS como fontes de feed OData](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
