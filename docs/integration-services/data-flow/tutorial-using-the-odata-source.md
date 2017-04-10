---
title: "Tutorial: Usando o OData Source | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Tutorial: Usando o OData Source
  Este tutorial orienta você pelo processo de extrair a coleção **Employees** do serviço de exemplo **Northwind** OData (http://services.odata.org/V3/Northwind/Northwind.svc/) e o carrega em um arquivo simples.  
  
## 1. Criar um projeto do Integration Services  
  
1.  Inicie o **SQL Server Data Tools** ou o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Clique em **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto**, expanda **Instalado**, **Modelos**, **Business Intelligence** e clique em **Integration Services**.  
  
4.  Selecione **Projeto do Integration Services** como tipo de projeto.  
  
5.  Insira um **nome** e selecione um **local** para o projeto e clique em **OK**.  
  
## 2. Adicionar e configurar OData Source ao pacote SSIS  
  
1.  Arraste e solte uma **Tarefa de Fluxo de Dados** da **Caixa de Ferramentas do SSIS** para a superfície de design de fluxo de controle do seu pacote SSIS.  
  
2.  Clique na guia **Fluxo de Dados** ou clique duas vezes na **Tarefa de Fluxo de Dados** recém-adicionada para iniciar a **superfície de design Fluxo de Dados**.  
  
3.  Arraste e solte o **OData Source** do grupo **Comum** para a **Caixa de Ferramentas do SSIS**. Quando o **OData Source** for instalado pela primeira vez, ele aparecerá sob o grupo **Comum** na **Caixa de Ferramentas do SSIS**.  
  
4.  Clique duas vezes no componente **OData Source** para iniciar a caixa de diálogo **Editor do OData Source**.  
  
5.  Clique em **Novo…** para adicionar um novo Gerenciador de Conexões OData.  
  
6.  Insira a URL do serviço OData para **Local do documento de serviço**. Essa pode ser a URL do documento do serviço ou para um feed ou a uma entidade específica. Para este tutorial, digite [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Verifique se a **Autenticação do Windows** está selecionada como **autenticação** a ser usada para acessar o serviço OData. A **Autenticação do Windows** está selecionada por padrão. Para usar a autenticação básica, selecione **Usar este nome de usuário e senha**.  
  
8.  Clique em **Testar Conexão** para a conexão e clique em **OK** para criar uma instância do Gerenciador de Conexões OData.  
  
9. Na caixa de diálogo **Editor do OData Source**, verifique se a opção **Coleção** está selecionada para **Usar coleção no caminho do recurso**.  
  
10. Na lista suspensa **Coleção**, selecione **Employees**.  
  
11. Insira as opções de consulta adicionais do OData ou filtros para **Opções de Consulta**. Ex. $orderby=CompanyName&$top=100. Para este tutorial, insira **$top=5**.  
  
12. Clique em **Visualizar** para visualizar os dados.  
  
13. Clique em **Colunas** no painel de navegação esquerdo para mudar para a página **Colunas**.  
  
14. Selecione **EmployeeID**, **FirstName** e **LastName** em **Colunas Externas Disponíveis** marcando as caixas de seleção.  
  
15. Clique em **OK** para fechar a caixa de diálogo **Editor do OData Source**.  
  
## 3. Adicionar o destino de arquivo simples e testar a solução  
  
1.  Agora, arraste e solte um **Destino de Arquivo Simples** da **Caixa de Ferramentas do SSIS** para a superfície de design de Fluxo de Dados abaixo do componente **OData Source**.  
  
2.  Conecte o componente **OData Source** ao componente **Destino de Arquivo Simples** usando a seta azul.  
  
3.  Clique duas vezes em **Destino de Arquivo Simples**. Você deve ver a caixa de diálogo **Editor de Destino de Arquivo Simples**.  
  
4.  Na caixa de diálogo **Editor de Destino de Arquivo Simples**, clique em **Novo** para criar um novo gerenciador de conexões de arquivo simples.  
  
5.  Na caixa de diálogo **Formato de Arquivo Simples**, selecione **Delimitado**. Você deve ver a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples**.  
  
6.  Na caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples**, como **Nome do Arquivo**, insira **c:\Employees.txt**.  
  
7.  No painel de navegação esquerdo, clique em **Colunas**. Você pode visualizar os dados nessa página.  
  
8.  Clique em OK para fechar a caixa de diálogo **Editor de Gerenciador de Conexões de Arquivo Simples**.  
  
9. Na caixa de diálogo **Editor de Destino de Arquivo Simples**, clique em **Mapeamentos** no painel de navegação esquerdo. Examine os mapeamentos.  
  
10. Clique em OK para fechar a caixa de diálogo **Editor de Destino de Arquivo Simples**.  
  
11. Compile e execute o pacote do SSIS. Verifique se o arquivo de saída foi criado com a ID, o Nome e o Sobrenome de 5 funcionários do feed do OData.  
  
  