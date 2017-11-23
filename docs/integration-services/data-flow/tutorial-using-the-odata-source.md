---
title: 'Tutorial: Usando o OData Source | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: cbdc4a2e0719e65e378d232c5abcb5404e8342f1
ms.contentlocale: pt-br
ms.lasthandoff: 08/23/2017

---
# <a name="tutorial-using-the-odata-source"></a>Tutorial: Usando o OData Source
  Este tutorial orienta você pelo processo de extrair a coleção **Employees** do serviço de exemplo **Northwind** OData (http://services.odata.org/V3/Northwind/Northwind.svc/) e o carrega em um arquivo simples.  
  
## <a name="1-create-an-integration-services-project"></a>1. Criar um projeto do Integration Services  
  
1.  Inicie o **SQL Server Data Tools** ou o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Clique em **Arquivo**, aponte para **Novo**e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto** , expanda **Instalado**, **Modelos**, **Business Intelligence**e clique em **Integration Services**.  
  
4.  Selecione **Projeto do Integration Services** como tipo de projeto.  
  
5.  Insira um **nome** e selecione um **local** para o projeto e clique em **OK**.  
  
## <a name="2-add-and-configure-an-odata-source"></a>2. Adicionar e configurar uma fonte OData 
  
1.  Arraste e solte uma **Tarefa de Fluxo de Dados** da **Caixa de Ferramentas do SSIS** para a superfície de design de fluxo de controle do seu pacote SSIS.  
  
2.  Clique o **de fluxo de dados** tab ou clique duas vezes no **a tarefa de fluxo de dados** para abrir a superfície de design de fluxo de dados.  
  
3.  Arraste e solte o **OData Source** do grupo **Comum** para a **Caixa de Ferramentas do SSIS**.
  
4.  Clique duas vezes o **fonte OData** componente para iniciar o **Editor de origem OData** caixa de diálogo.  
  
5.  Clique em **Novo…** para adicionar um novo Gerenciador de Conexões OData.  
  
6.  Insira a URL do serviço OData para **Local do documento de serviço**. Essa URL pode ser a URL para o documento de serviço ou para um feed específico ou uma entidade. Para fins deste tutorial, insira a URL para o documento de serviço: [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Verifique se a **Autenticação do Windows** está selecionada como **autenticação** a ser usada para acessar o serviço OData. A**Autenticação do Windows** está selecionada por padrão.  
  
8.  Clique em **Testar Conexão** para testar a conexão e clique em **Okey** para concluir a criação de uma instância do Gerenciador de Conexão do OData.  
  
9. Na caixa de diálogo **Editor do OData Source** , verifique se a opção **Coleção** está selecionada para **Usar coleção no caminho do recurso** .  
  
10. Do **coleção** lista suspensa, selecione **funcionários**.  
  
11. Insira as opções de consulta adicionais do OData ou filtros para **Opções de Consulta**. Por exemplo, `$orderby=CompanyName&$top=100`. Para fins deste tutorial, insira `$top=5`.  
  
12. Clique em **Visualizar** para visualizar os dados.  
  
13. Clique em **Colunas** no painel de navegação esquerdo para mudar para a página **Colunas** .  
  
14. Selecione **EmployeeID**, **FirstName**e **LastName** em **Colunas Externas Disponíveis** marcando as caixas de seleção.  
  
15. Clique em **OK** para fechar a caixa de diálogo **Editor do OData Source**.  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3. Adicionar e configurar um destino de arquivo simples
  
1.  Agora, arraste e solte um **Destino de Arquivo Simples** da **Caixa de Ferramentas do SSIS** para a superfície de design de Fluxo de Dados abaixo do componente **OData Source**.  
  
2.  Conecte o componente **OData Source** ao componente **Destino de Arquivo Simples** usando a seta azul.  
  
3.  Clique duas vezes em **Destino de Arquivo Simples**. Você deve ver a caixa de diálogo **Editor de Destino de Arquivo Simples** .  
  
4.  Na caixa de diálogo **Editor de Destino de Arquivo Simples** , clique em **Novo** para criar um novo gerenciador de conexões de arquivo simples.  
  
5.  Na caixa de diálogo **Formato de Arquivo Simples** , selecione **Delimitado**. Em seguida, você vê o **Editor do Gerenciador de Conexão de arquivo simples** caixa de diálogo.  
  
6.  No **Editor do Gerenciador de Conexão de arquivo simples** caixa de diálogo, para o **nome de arquivo**, digite `c:\Employees.txt`.  
  
7.  No painel de navegação esquerdo, clique em **Colunas**. Você pode visualizar os dados nessa página.  
  
8.  Clique em OK para fechar a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples** .  
  
9. Na caixa de diálogo **Editor de Destino de Arquivo Simples** , clique em **Mapeamentos** no painel de navegação esquerdo. Examine os mapeamentos.  
  
10. Clique em OK para fechar a caixa de diálogo **Editor de Destino de Arquivo Simples** .  

## <a name="4-run-the-package"></a>4. Execute o pacote
Execute o pacote do SSIS. Verifique se o arquivo de saída é criado com a ID, nome, sobrenome para cinco funcionários do OData feed.
  
  

