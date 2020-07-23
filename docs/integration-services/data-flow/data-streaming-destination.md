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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3dd1ae26ab126e87a8f239597a573d24dbc8b3e1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916745"
---
# <a name="data-streaming-destination"></a>Destino do Fluxo de Dados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O **Destino do Streaming de Dados** é um componente de destino do SSIS ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) que permite que o **Provedor OLE DB para SSIS** consuma a saída de um pacote SSIS como um conjunto de resultados de tabelas. Você pode criar um servidor vinculado que use o Provedor OLE DB para SSIS e então execute uma consulta SQL no servidor vinculado para exibir os dados retornados pelo pacote SSIS.  
  
 No exemplo a seguir, a consulta a seguir retorna a saída do pacote Package.dtsx no projeto SSISPackagePublishing na pasta do Power BI do Catálogo do SSIS. Essa consulta usa o servidor vinculado chamado [Servidor Vinculado Padrão para o Integration Services] que, por sua vez, usa o novo Provedor OLE DB para SSIS. A consulta inclui o nome da pasta, o nome do projeto e o nome do pacote no catálogo do SSIS. O Provedor OLE DB para SSIS executa o pacote especificado na consulta e retorna o conjunto de resultados tabulares.  
  
```sql
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Componentes de publicação de feed de dados  
 Os Componentes de publicação de feed de dados incluem: Provedor OLE DB para SSIS, Destino do Streaming de Dados e o Assistente de Publicação de Pacote do SSIS. O assistente permite que você publique um pacote do SSIS como uma exibição SQL em uma instância de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O assistente ajuda você na criação de um servidor vinculado que use o Provedor OLE DB para SSIS e uma exibição SQL que representa uma consulta no servidor vinculado. Execute a exibição para consultar os resultados do pacote do SSIS como um conjunto de dados tabulares.  
  
 Para confirmar se o provedor SSISOLEDB está instalado no SQL Server Management Studio, expanda **Objetos de Servidor**, **Servidores Vinculados**, **Provedores**e confirme se o provedor **SSISOLEDB** é exibido. Clique duas vezes em **SSISOLEDB**, habilite **Permitir Inprocess** se ele não estiver habilitado e clique em **OK**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Publicar um pacote do SSIS como uma exibição SQL  
 O procedimento a seguir descreve as etapas para publicar um pacote do SSIS como uma exibição do SQL.  
  
1.  Crie um pacote do SSIS com um componente de **Destino do Fluxo de Dados** e implante o pacote no Catálogo do SSIS.  
  
2.  Execute o **Assistente de Publicação de Pacote do SSIS** executando ISDataFeedPublishingWizard.exe em C:\Arquivos de Programas\Microsoft SQL Server\130\DTS\Binn ou executando o Assistente de Publicação de Feed de Dados do menu Iniciar.  
  
     O assistente cria um servidor vinculado usando o SSISOLEDB (Provedor OLE DB para SSIS) e cria uma exibição SQL que consiste em uma consulta no servidor vinculado. Essa consulta inclui o nome da pasta, o nome do projeto e o nome do pacote no catálogo do SSIS.  
  
3.  Execute a exibição SQL no SQL Server Management Studio e verifique os resultados do pacote do SSIS. A exibição envia a consulta para o Provedor OLE DB para SSIS por meio do servidor vinculado criado por você. O Provedor OLE DB para SSIS executa o pacote especificado na consulta e retorna o conjunto de resultados tabulares.  
  
> [!IMPORTANT]  
>  Para obter etapas detalhadas, veja [Passo a passo: publicar um pacote do SSIS como uma exibição SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  

## <a name="configure-data-streaming-destination"></a>Configurar destino do fluxo de dados
  Configure o destino de fluxo de dados usando a caixa de diálogo **Editor Avançado para o Destino do Fluxo de Dados** . Abra essa caixa de diálogo clicando duas vezes no componente ou clicando com o botão direito do mouse no componente, no designer de fluxo de dados, e clicando em **Editar**.  
  
 Essa caixa de diálogo tem três guias: **Propriedades do Componente**, **Colunas de Entrada** e **Propriedades de Entrada e Saída**.  
  
## <a name="component-properties-tab"></a>Guia Propriedades do Componente  
 Esta guia tem os seguintes campos editáveis:  
  
|Campo|Descrição|  
|-----------|-----------------|  
|Nome|Nome do componente de destino de streaming de dados no pacote.|  
|ValidateExternalMetadata|Indica se o componente é validado usando fontes de dados externas no momento do design. Se definido como falso, a validação das fontes de dados externas é atrasada até o runtime.|  
|IDColumnName|A exibição gerada pelo Assistente de publicação de feed de dados tem esta coluna de ID adicional. A coluna ID serve como EntityKey para os dados de saída do fluxo de dados quando os dados são consumidos como um feed de OData por outros aplicativos.<br /><br /> O nome padrão para esta coluna é _ID. Você pode especificar um nome diferente para a coluna de ID.|  
  
## <a name="input-columns-tab"></a>Guia Colunas de Entrada  
 No painel superior dessa guia, você deve ver todas as colunas de entrada disponíveis. Selecione as colunas que você deseja incluir na saída deste componente. As colunas selecionadas são exibidas em uma lista no painel inferior. Você pode alterar o nome da coluna de saída, digitando o novo nome no campo **Alias de Saída** na lista.  
  
## <a name="input-output-properties-tab"></a>Guia Propriedades de Entrada e Saída  
 Semelhante à guia Colunas de Entrada, você pode alterar os nomes das colunas de saída nesta guia. No modo de exibição de árvore à esquerda, expanda **Entrada de Destino do Streaming de Dados** e expanda **Colunas de Entrada**. Clique no nome da coluna de entrada e altere o nome do nome da coluna de saída no painel à direita.
