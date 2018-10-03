---
title: Gerenciamento de informações da empresa usando SSIS, MDS e DQS em conjunto [Tutorial] | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d03470d21532ce097ba753fb8073a5685ccb9f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122626"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Gerenciamento de informações da empresa usando o SSIS, o MDS e o DQS em conjunto [Tutorial]
  O gerenciamento de informações em uma empresa normalmente envolve a integração dos dados na empresa e fora dela, a limpeza dos dados, a correspondência dos dados para remover qualquer duplicata, a padronização dos dados, o enriquecimento dos dados, a adequação dos dados com os requisitos legais e de conformidade e o armazenamento do dados em um local centralizado com todas as configurações de segurança necessárias.  
  
 O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] fornece todos os componentes necessários para uma solução efetiva de Gerenciamento de Informações da Empresa (EIM) em um único produto. Estes são os principais componentes que ajudam a criar uma solução EIM:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 O SQL Server Integration Services (SSIS) fornece uma plataforma sofisticada e extensível para a integração de dados de várias fontes em uma solução de extração, transformação e carregamento (ETL) abrangente que oferece suporte a fluxos de trabalho comerciais, data warehouse ou gerenciamento de dados mestre. Ver [visão geral dos serviços de integração](http://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) tópico para obter uma visão geral e típico usa do SSIS.  
  
 O SQL Server Data Quality Services (DQS) permite a limpeza, a correspondência, a padronização e o enriquecimento dos dados; portanto, é possível enviar informações confiáveis para business intelligence, data warehouse e cargas de trabalho de processamento de transações. Ver [Introdução ao Data Quality Services](http://msdn.microsoft.com/library/ff877917.aspx) tópico para a necessidade comercial do DQS e como ele responde a necessidade.  
  
 O SQL Server Master Data Services (MDS) fornece um hub de dados central que assegura a constante integridade das informações e consistência dos dados entre diferentes aplicativos. Ver [visão geral do Master Data Services](../master-data-services/master-data-services-overview-mds.md) tópico para obter descrições resumidas dos recursos importantes do MDS.  
  
 Ver [limpeza e correspondência de dados mestre usando tecnologias de EIM](http://msdn.microsoft.com/library/hh403491.aspx) white papers para obter uma orientação abrangente sobre como implementar uma solução EIM usando essas tecnologias do Microsoft EIM juntos e assista [Enterprise Gerenciamento de informações (EIM): Reunindo o SSIS, DQS e MDS](http://go.microsoft.com/fwlink/?LinkId=258672) vídeo para ver uma demonstração interessante de um cenário de EIM.  
  
 Neste tutorial, você aprenderá a usar o SSIS, o MDS e o DQS em conjunto para implementar um exemplo de solução de Gerenciamento de informações da empresa (EIM). Primeiro, use o DQS para criar uma base de dados de conhecimento que contenha informações sobre os dados (metadados), limpar os dados em um arquivo do Excel usando a base de dados de conhecimento, e fazer a correspondência dos dados para identificar e remover duplicatas. Em seguida, use o Suplemento MDS para Excel a fim de carregar os dados limpos e correspondentes no MDS. Depois, automatize todo o processo usando uma solução SSIS. A solução SSIS neste tutorial lê os dados de entrada de um arquivo do Excel, mas é possível estendê-lo para que essa leitura seja feita de várias fontes, como o Oracle, o Teradata, o DB2 e o Banco de dados SQL do Windows Azure.  
  
## <a name="prerequisites"></a>Prerequisites  
  
1.  Microsoft SQL Server 2012 com os seguintes componentes instalados.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Ver [guia de instalação do SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) para obter detalhes sobre como instalar o produto.  
  
2.  [Configurar MDS usando o Gerenciador de configuração do Master Data Services](http://msdn.microsoft.com/library/ee633884.aspx)  
  
     Use o Gerenciador de Configuração para criar e configura um banco de dados do Master Data Services. Depois de criar o banco de dados do MDS, crie um aplicativo web para o MDS em um site da web (por exemplo: [ http://localhost/MDS ](http://localhost/MDS)) e associe o banco de dados do MDS ao aplicativo web do MDS. Observe que, para criar um aplicativo Web do MDS, você deve ter o IIS instalado no computador. Ver [requisitos do aplicativo Web (Master Data Services)](http://msdn.microsoft.com/library/ee633744.aspx) e [requisitos de banco de dados (Master Data Services)](http://msdn.microsoft.com/library/ee633767.aspx) para obter detalhes sobre os pré-requisitos para configurar o aplicativo web e banco de dados do MDS.  
  
3.  [Instalar e configurar o DQS usando o instalador do Data Quality](http://msdn.microsoft.com/library/hh231682.aspx). Clique em **inicie**, clique em **todos os programas**, clique em **Microsoft SQL Server 2014**, clique em **Data Quality Services**e, em seguida, clique em **Instalador do data Quality**.  
  
4.  Microsoft Excel 2010 (32 bits é preferencial).  
  
5.  Instale **suplemento Master Data Services para Excel** (32 bits ou 64 bits com base na versão do Excel que você tem em seu computador) de [aqui](http://www.microsoft.com/download/details.aspx?id=29064). Para localizar a versão do Excel instalado em seu computador, execute **Excel**, clique em **arquivo** na barra de menus e clique em **ajuda** para ver a versão no painel direito. Observe que você precisa instalar o Visual Studio 2010 Tools for Office Runtime antes de instalar o suplemento do Excel.  
  
6.  (Opcional) Crie uma conta com [Windows Azure Marketplace](https://datamarket.azure.com/). Uma das tarefas no tutorial exige que você tenha um **do Azure Marketplace** (originalmente denominado **Data Market**) conta. Você poderá ignorar essa tarefa se desejar e passar para a próxima tarefa.  
  
7.  Baixe o arquivo Suppliers. xls do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=271504).  
  
8.  O DQS não permite a exportação de limpeza ou correspondência de resultados para um arquivo do Excel se você estiver usando **versão de 64 bits do Excel**. Esse é um problema conhecido. Para resolvê-lo, faça o seguinte:  
  
    1.  Execute **DQLInstaller.exe – atualizar**. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Clique duas vezes no arquivo DQSInstaller.exe.  
  
    2.  Na **Gerenciador de configuração do Master Data Services**, clique em **Selecionar banco de dados**, selecione existente **MDS** banco de dados e, em seguida, clique em **atualizar**.  
  
## <a name="lessons"></a>Lições  
  
|Lição|Breve descrição|Tempo estimado para concluir (em minutos).|  
|------------|-----------------------|------------------------------------------------|  
|[Lição 1: Criando a base de dados de conhecimento do DQS de fornecedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|Nesta lição, você criará uma base de dados de conhecimento do DQS denominada **fornecedores**.|60|  
|[Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|Nesta lição, você pode criar e executar um projeto do DQS para limpar os dados do fornecedor em um arquivo do Excel usando o **fornecedores** Base de dados de conhecimento que você criou na primeira lição.|45|  
|[Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|Nesta lição, você criará um projeto do DQS para executar a atividade de correspondência a fim de identificar e remover duplicatas da lista de fornecedores limpa.|45|  
|[Lição 4: Armazenando dados do fornecedor no MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|Nesta lição, você carregará os dados de fornecedor limpos e correspondentes para serviços de dados mestre (MDS) usando o **o suplemento MDS para Excel**.|45|  
|[Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|Nesta lição, você criará uma solução SSIS que limpa os dados de entrada usando o DQS, faz a correspondência dos dados limpos para remover duplicatas, e armazena os dados limpos e correspondentes no MDS de forma automatizada.|75|  
  
## <a name="next-steps"></a>Próximas etapas  
 Para começar o tutorial, vá para a primeira lição: [lição 1: Criando a Base de dados de conhecimento do DQS fornecedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
