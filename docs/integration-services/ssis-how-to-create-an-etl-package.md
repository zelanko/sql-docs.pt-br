---
title: "SSIS: Como criar um pacote ETL | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "SSIS, tutoriais"
  - "pacotes [Integration Services], tutoriais"
  - "Integration Services, tutoriais"
  - "SQL Server Integration Services, tutoriais"
  - "logs [Integration Services], tutoriais"
  - "instruções passo a passo [Integration Services]"
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# SSIS: Como criar um pacote ETL
[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] O SSIS é uma plataforma para a criação de soluções para integração de dados de alto desempenho, incluindo também pacotes ETL (extração, transformação e carregamento) para armazenamento de dados. O SSIS inclui ferramentas gráficas e assistentes para criação e depuração de pacotes; tarefas para execução de funções de fluxo de trabalho como, por exemplo, operações de FTP, execução de instruções SQL e envio de mensagens de email; fontes de dados e destinos para extração e carregamento de dados; transformações para limpeza, agregação, junção e cópia de dados; um serviço de gerenciamento, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administração de execução e armazenamento de pacotes; e APIs (interfaces de programação de aplicativo) para programação do modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
Neste tutorial, você aprenderá a usar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para criar um pacote simples do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O pacote que você cria conduz dados de um arquivo simples, formata esses dados e insere os dados formatados em uma tabela de fatos. Nas lições a seguir, o pacote é expandido para demonstrar looping, configurações de pacote, registro de log e fluxo de erros.  
  
Ao instalar os dados de exemplo usados pelo tutorial, as versões concluídas dos pacotes criados para cada lição do tutorial também são instaladas. Ao utilizar os pacotes concluídos, será possível começar o tutorial em uma lição posterior, caso queira. Se esta for a primeira vez que você trabalha com pacotes ou com o novo ambiente de desenvolvimento, recomendamos que você comece pela lição 1.  
  
## O que você aprenderá  
O melhor modo de familiarizar-se com as novas ferramentas, controles e recursos disponíveis no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é utilizando-os. Este tutorial explicará como usar o Designer de [!INCLUDE[ssIS](../includes/ssis-md.md)] para criar um pacote de ETL simples com looping, configurações, lógica de fluxo de erros e registro de logs.  
  
## Requisitos  
O tutorial é destinado a usuários familiarizados com operações básicas de banco de dados, mas que tiveram pouca experiência com os novos recursos disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o banco de dados **AdventureWorksDW2012** . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão. Para baixar o banco de dados **AdventureWorksDW2012** , consulte [Adventure Works para SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=275026).  
  
    > [!IMPORTANT]  
    > Quando você anexa o banco de dados (arquivo \*.mdf), o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pesquisará por padrão um arquivo .ldf. Você deve remover manualmente o arquivo .ldf antes de clicar em OK na caixa de diálogo **Anexar Bancos de Dados** .  
    >   
    > Para obter mais informações sobre como anexar bancos de dados, consulte [Attach a Database](../relational-databases/databases/attach-a-database.md).  
  
-   Dados de exemplo. Os dados de exemplo estão incluídos com os pacotes de lição do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para baixar os dados de exemplo e os pacotes de lição, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
## Lições neste tutorial  
[Lição 1: Criar um projeto e pacote básico com o SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
Nesta lição, você criará um pacote de ETL simples que extrairá dados de um arquivo simples, transformará os dados usando transformações de pesquisa e, por fim, carregará o resultado em um destino da tabela de fatos.  
  
[Lição 2: Adicionando um loop com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na Lição 1 para tirar proveito dos novos recursos de looping para extrair arquivos simples múltiplos em um único processo de fluxo de dados.  
  
[Lição 3: Adicionar o log com o SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 2 para usar as novas opções de registro de logs.  
  
[Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 3 para usar as novas opções de configuração das saídas de erro.  
  
[Lição 5: Adicionar configurações do pacote SSIS ao modelo de implantação de pacotes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
Nesta lição, você expandirá o pacote criado na lição 4 para usar as novas opções de configuração de pacote.  
  
[Lição 6: Usando parâmetros com o modelo de implantação de projetos no SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 5 para usar os novos parâmetros com o modelo de implantação de projeto.  
  
  
  
