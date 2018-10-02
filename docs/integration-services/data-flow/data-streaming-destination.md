---
title: Destino do Streaming de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 958446082e1576e14f50d09a9b8b7181bf2f18af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771574"
---
# <a name="data-streaming-destination"></a>Destino do Fluxo de Dados
  O **Destino do Fluxo de Dados** é um componente de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS), que permite que o **Provedor OLE DB para SSIS** consuma a saída de um pacote SSIS como um conjunto de resultados de tabelas. Você pode criar um servidor vinculado que use o Provedor OLE DB para SSIS e então execute uma consulta SQL no servidor vinculado para exibir os dados retornados pelo pacote SSIS.  
  
 No exemplo a seguir, a consulta a seguir retorna a saída do pacote Package.dtsx no projeto SSISPackagePublishing na pasta do Power BI do Catálogo do SSIS. Essa consulta usa o servidor vinculado chamado [Servidor Vinculado Padrão para o Integration Services] que, por sua vez, usa o novo Provedor OLE DB para SSIS. A consulta inclui o nome da pasta, o nome do projeto e o nome do pacote no catálogo do SSIS. O Provedor OLE DB para SSIS executa o pacote especificado na consulta e retorna o conjunto de resultados tabulares.  
  
```sql
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
  
-   [Passo a passo: publicar um pacote SSIS como uma exibição SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
## <a name="configure-data-streaming-destination"></a>Configurar destino do fluxo de dados
  Configure o destino de fluxo de dados usando a caixa de diálogo **Editor Avançado para o Destino do Fluxo de Dados** . Abra essa caixa de diálogo clicando duas vezes no componente ou clicando com o botão direito do mouse no componente, no designer de fluxo de dados, e clicando em **Editar**.  
  
 A caixa de diálogo tem três guias: **Propriedades do Componente**, **Colunas de Entrada**, e **Propriedades de Entrada e Saída**.  
  
## <a name="component-properties-tab"></a>Guia Propriedades do Componente  
 Esta guia tem os seguintes campos editáveis:  
  
|Campo|Descrição|  
|-----------|-----------------|  
|Nome|Nome do componente de destino de streaming de dados no pacote.|  
|ValidateExternalMetadata|Indica se o componente é validado usando fontes de dados externas no momento do design. Se definido como falso, a validação das fontes de dados externas é atrasada até o tempo de execução.|  
|IDColumnName|A exibição gerada pelo Assistente de publicação de feed de dados tem esta coluna de ID adicional. A coluna ID serve como EntityKey para os dados de saída do fluxo de dados quando os dados são consumidos como um feed de OData por outros aplicativos.<br /><br /> O nome padrão para esta coluna é _ID. Você pode especificar um nome diferente para a coluna de ID.|  
  
## <a name="input-columns-tab"></a>Guia Colunas de Entrada  
 No painel superior dessa guia, você deve ver todas as colunas de entrada disponíveis. Selecione as colunas que você deseja incluir na saída deste componente. As colunas selecionadas são exibidas em uma lista no painel inferior. Você pode alterar o nome da coluna de saída, digitando o novo nome no campo **Alias de Saída** na lista.  
  
## <a name="input-output-properties-tab"></a>Guia Propriedades de Entrada e Saída  
 Semelhante à guia Colunas de Entrada, você pode alterar os nomes das colunas de saída nesta guia. No modo de exibição de árvore à esquerda, expanda **Entrada de Destino do Streaming de Dados** e expanda **Colunas de Entrada**. Clique no nome da coluna de entrada e altere o nome do nome da coluna de saída no painel à direita.  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar pacotes do SSIS como fontes de feed OData](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
