---
title: "Criar e modificar fontes de dados inseridas | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 10
---
# Criar e modificar fontes de dados inseridas
  Um fonte de dados inserida é definida em uma definição de relatório e usada apenas por esse relatório.  
  
## Para criar uma fonte de dados inserida no Designer de Relatórios  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, clique em **Dados do Relatório** no menu **Exibir**.  
  
2.  Na caixa de texto **Nome**, digite um nome para a fonte de dados ou aceite o padrão. O nome da fonte de dados é usado internamente no relatório. Para fins de esclarecimento, recomendamos que o nome da fonte de dados contenha o nome do banco de dados especificado na cadeia de conexão.  
  
3.  Verifique se a opção **Conexão inserida** está marcada e faça o seguinte.  
  
    1.  Na lista suspensa **Tipo**, selecione um tipo de fonte de dados; por exemplo, **Microsoft SQL Server** ou **OLE DB**.  
  
    2.  Especifique uma cadeia de conexão usando uma das seguintes alternativas:  
  
        -   Digite a cadeia de conexão diretamente na caixa de texto **Cadeia de conexão**. Para obter uma lista de exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md) ou [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Clique no botão de expressão (**fx)** para criar uma expressão que seja avaliada como uma cadeia de conexão. Na caixa de diálogo **Expressão**, digite a expressão no painel Expressão. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Clique em **Editar** para abrir a caixa de diálogo **Propriedades de Conexão** para o tipo de fonte de dados escolhido na etapa 2.  
  
             Preencha os campos na caixa de diálogo **Propriedades de Conexão**, conforme adequado, para o tipo de fonte de dados. As propriedades de conexão incluem o tipo de fonte de dados, o nome da fonte de dados e as credenciais a serem usadas. Depois de especificar valores nesta caixa de diálogo, clique em **Testar Conexão** para verificar se a fonte de dados está disponível e se as credenciais especificadas estão corretas. Para obter mais informações sobre tipos de fonte de dados específicos, consulte os tópicos [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
    3.  Clique em **Credenciais**.  
  
         Especifique as credenciais que serão usadas para essa fonte de dados. O proprietário da fonte de dados escolhe o tipo de credenciais com suporte.  
  
4.  A nova fonte de dados inserida será exibida no painel Dados do Relatório.  
  
## Para criar uma fonte de dados inserida no Construtor de Relatórios  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Na caixa de texto **Nome**, digite um nome para a fonte de dados ou aceite o padrão.  
  
3.  Verifique se a opção **Usar uma conexão inserida em meu relatório** está marcada.  
  
    1.  Na lista suspensa **Selecionar o tipo de conexão**, selecione um tipo de fonte de dados; por exemplo, **Microsoft SQL Server** ou **OLE DB**.  
  
    2.  Especifique uma cadeia de conexão usando uma das alternativas a seguir:  
  
        -   Digite a cadeia de conexão diretamente na caixa de texto **Cadeia de conexão**. Para obter uma lista de exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
        -   Clique no botão de expressão (**fx)** para criar uma expressão que seja avaliada como uma cadeia de conexão. Na caixa de diálogo **Expressão**, digite a expressão no painel Expressão. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Clique em **Criar** para abrir a caixa de diálogo **Propriedades de Conexão** para o tipo de fonte de dados escolhido na etapa 2.  
  
             Preencha os campos na caixa de diálogo **Propriedades de Conexão**, conforme adequado, para o tipo de fonte de dados. As propriedades de conexão incluem o tipo de fonte de dados, o nome da fonte de dados e as credenciais a serem usadas. Depois de especificar valores nesta caixa de diálogo, clique em **Testar Conexão** para verificar se a fonte de dados está disponível e se as credenciais especificadas estão corretas.  
  
4.  Clique em **Credenciais**.  
  
     Especifique as credenciais que serão usadas para essa fonte de dados. O proprietário da fonte de dados escolhe o tipo de credenciais com suporte. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     A fonte de dados será exibida no painel de dados do relatório.  
  
## Consulte também  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Especificar as credenciais no Construtor de Relatórios](../Topic/Specify%20Credentials%20in%20Report%20Builder.md)  
  
  