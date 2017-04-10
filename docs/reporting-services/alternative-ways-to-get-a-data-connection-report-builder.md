---
title: "Formas alternativas de obter uma conex&#227;o de dados (Construtor de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "06/15/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Formas alternativas de obter uma conex&#227;o de dados (Construtor de Relat&#243;rios)
Uma conexão de dados contém as informações para estabelecer conexões com uma fonte de dados externa, como um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Geralmente, você obtém as informações sobre a conexão e o tipo de credenciais a ser usado do proprietário da fonte de dados.  
  
Para especificar uma conexão de dados, é possível usar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida que será usada somente em um relatório específico.  
  
Na maioria dos tutoriais, você usa fontes de dados inseridas, mas se tiver acesso a fontes de dados compartilhadas, você poderá usá-las.  
  
## Obtendo uma conexão de dados de uma fonte de dados compartilhada  
Se o servidor de relatório tiver fontes de dados compartilhadas disponíveis que você tenha permissão para usar, use-as em vez de uma fonte de dados inserida. Os procedimentos a seguir explicam como localizar as fontes de dados compartilhadas e como fornecer todas as credenciais necessárias para usá-las.  
  
Para usar uma fonte de dados compartilhada, procure um servidor de relatório e selecione-o. Geralmente, você obtém o URL do servidor de relatório do administrador do servidor de relatório.  
  
### Para especificar uma conexão de dados de uma lista de fontes de dados compartilhadas  
  
1.  No Assistente de Nova Tabela ou Matriz ou no Assistente de Novo Gráfico, na página **Escolher um conjunto de dados**, selecione **Criar um conjunto de dados** e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Na lista de fontes de dados, selecione uma que você tenha permissão para acessar.  
  
3.  Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**. A mensagem "Conexão criada com êxito" será exibida. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Clique em **Avançar**.  
  
    Se necessário, insira suas credenciais. Para salvar as credenciais localmente, selecione **Salvar senha com a conexão**. Se você não selecionar essa opção, será solicitado que você insira as credenciais sempre que executar o relatório  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### Para especificar uma conexão de dados navegando até uma fonte de dados compartilhada em um servidor de relatório  
  
1.  No Assistente de Nova Tabela ou Matriz ou no Assistente de Novo Gráfico, na página **Escolher um conjunto de dados**, selecione **Criar um conjunto de dados** e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Clique em **Procurar**. A caixa de diálogo **Selecionar Fonte de Dados** é aberta.  
  
3.  Na lista suspensa **Examinar**, selecione **Sites e Servidores Recentes**. No painel da fonte de dados, clique na URL do servidor e em **Abrir**.  
  
    A lista de fontes de dados ou modelos é exibida.  
  
4.  Como alternativa, em **Nome**, digite a URL do servidor de relatório. Clique em **Abrir**.  
  
    O Construtor de Relatórios é conectado ao servidor de relatório e carrega as fontes de dados disponíveis na pasta raiz.  
  
5.  Navegue até uma pasta que contém uma fonte de dados à qual você tenha permissões suficientes para se conectar, selecione-a e clique em **Abrir**.  
  
    Você voltará à página **Escolher uma conexão com uma fonte de dados**.  
  
6.  Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
    A mensagem "Conexão criada com êxito" será exibida. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique em **Avançar**.  
  
8.  Se for solicitado que você informe um nome de usuário e uma senha, insira suas credenciais. Para salvar as credenciais localmente, selecione **Salvar senha com a conexão**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## Consulte também  
[Conjuntos de dados de relatório &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md) 
  
