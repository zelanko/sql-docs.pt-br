---
title: 'Tutorial: uso do OData Source| Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 95dceade62e487db05a66df6b7986f23723b1303
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297765"
---
# <a name="tutorial-using-the-odata-source"></a>Tutorial: Usando o OData Source

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Este tutorial orienta você pelo processo de extrair a coleção **Funcionários** do serviço **Northwind** OData de amostra (https://services.odata.org/V3/Northwind/Northwind.svc/) e, em seguida, carregue-o para um arquivo simples.  
  
## <a name="1-create-an-integration-services-project"></a>1. Criar um projeto do Integration Services  
  
1.  Inicie o **SQL Server Data Tools** ou o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Clique em **Arquivo**, aponte para **Novo**e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto** , expanda **Instalado**, **Modelos**, **Business Intelligence**e clique em **Integration Services**.  
  
4.  Selecione **Projeto do Integration Services** como tipo de projeto.  
  
5.  Insira um **nome** e selecione um **local** para o projeto e clique em **OK**.  
  
## <a name="2-add-and-configure-an-odata-source"></a>2. Adicionar e configurar um OData Source 
  
1.  Arraste e solte uma **Tarefa de Fluxo de Dados** da **Caixa de Ferramentas do SSIS** para a superfície de design de fluxo de controle do seu pacote SSIS.  
  
2.  Clique na guia **Fluxo de Dados** ou clique duas vezes na **Tarefa de Fluxo de Dados** para abrir a superfície de design de Fluxo de Dados.  
  
3.  Arraste e solte o **OData Source** do grupo **Comum** para a **Caixa de Ferramentas do SSIS**.
  
4.  Clique duas vezes no componente **OData Source** para iniciar a caixa de diálogo **Editor do OData Source**.  
  
5.  Clique em **Novo...** para adicionar um novo Gerenciador de Conexões OData.  
  
6.  Insira a URL do serviço OData para **Local do documento de serviço**. Essa URL pode ser igual àquela do documento do serviço ou à de um feed ou entidade específica. Para os fins deste tutorial, insira a URL para o documento de serviço: [https://services.odata.org/V3/Northwind/Northwind.svc/](https://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Verifique se a **Autenticação do Windows** está selecionada como **autenticação** a ser usada para acessar o serviço OData. A**Autenticação do Windows** está selecionada por padrão.  
  
8.  Clique em **Testar Conexão** para testar a conexão e clique em **OK** para criar uma instância do Gerenciador de Conexões OData.  
  
9. Na caixa de diálogo **Editor do OData Source** , verifique se a opção **Coleção** está selecionada para **Usar coleção no caminho do recurso** .  
  
10. Na lista suspensa **Coleção**, selecione **Funcionários**.  
  
11. Insira as opções de consulta adicionais do OData ou filtros para **Opções de Consulta**. Por exemplo, `$orderby=CompanyName&$top=100`. Para os fins deste tutorial, insira `$top=5`.  
  
12. Clique em **Visualizar** para visualizar os dados.  
  
13. Clique em **Colunas** no painel de navegação esquerdo para mudar para a página **Colunas** .  
  
14. Selecione **EmployeeID**, **FirstName**e **LastName** em **Colunas Externas Disponíveis** marcando as caixas de seleção.  
  
15. Clique em **OK** para fechar a caixa de diálogo **Editor do OData Source**.  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3. Adicionar e configurar um destino de arquivo simples
  
1.  Agora, arraste e solte um **Destino de Arquivo Simples** da **Caixa de Ferramentas do SSIS** para a superfície de design de Fluxo de Dados abaixo do componente **OData Source** .  
  
2.  Conecte o componente **OData Source** ao componente **Destino de Arquivo Simples** usando a seta azul.  
  
3.  Clique duas vezes em **Destino de Arquivo Simples**. Você deve ver a caixa de diálogo **Editor de Destino de Arquivo Simples** .  
  
4.  Na caixa de diálogo **Editor de Destino de Arquivo Simples** , clique em **Novo** para criar um novo gerenciador de conexões de arquivo simples.  
  
5.  Na caixa de diálogo **Formato de Arquivo Simples** , selecione **Delimitado**. Em seguida, você verá a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples**.  
  
6.  Na caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples**, como **Nome do arquivo**, insira `c:\Employees.txt`.  
  
7.  No painel de navegação esquerdo, clique em **Colunas**. Você pode visualizar os dados nessa página.  
  
8.  Clique em OK para fechar a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples** .  
  
9. Na caixa de diálogo **Editor de Destino de Arquivo Simples** , clique em **Mapeamentos** no painel de navegação esquerdo. Examine os mapeamentos.  
  
10. Clique em OK para fechar a caixa de diálogo **Editor de Destino de Arquivo Simples** .  

## <a name="4-run-the-package"></a>4. Executar o pacote
Execute o pacote SSIS. Verifique se o arquivo de saída foi criado com a ID, o Nome e o Sobrenome de cinco funcionários do feed do OData.
  
  
