---
title: Gerenciamento de informações corporativas usando SSIS, MDS e DQS juntos [Tutorial] | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 47bb74bf5fd35696481a88c4ccc30a8733f257a2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153557"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Gerenciamento de informações da empresa usando o SSIS, o MDS e o DQS em conjunto [Tutorial]
  O gerenciamento de informações em uma empresa normalmente envolve a integração dos dados na empresa e fora dela, a limpeza dos dados, a correspondência dos dados para remover qualquer duplicata, a padronização dos dados, o enriquecimento dos dados, a adequação dos dados com os requisitos legais e de conformidade e o armazenamento do dados em um local centralizado com todas as configurações de segurança necessárias.  
  
 O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] fornece todos os componentes necessários para uma solução efetiva de Gerenciamento de Informações da Empresa (EIM) em um único produto. Estes são os principais componentes que ajudam a criar uma solução EIM:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 O SQL Server Integration Services (SSIS) fornece uma plataforma sofisticada e extensível para a integração de dados de várias fontes em uma solução de extração, transformação e carregamento (ETL) abrangente que oferece suporte a fluxos de trabalho comerciais, data warehouse ou gerenciamento de dados mestre. Consulte [Integration Services tópico de visão geral](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) para obter uma visão geral rápida e usos típicos do SSIS.  
  
 O SQL Server Data Quality Services (DQS) permite a limpeza, a correspondência, a padronização e o enriquecimento dos dados; portanto, é possível enviar informações confiáveis para business intelligence, data warehouse e cargas de trabalho de processamento de transações. Consulte o tópico [apresentando o Data Quality Services](https://msdn.microsoft.com/library/ff877917.aspx) para obter a necessidade comercial do DQS e como o DQS responde à necessidade.  
  
 O SQL Server Master Data Services (MDS) fornece um hub de dados central que assegura a constante integridade das informações e consistência dos dados entre diferentes aplicativos. Consulte [Master Data Services tópico de visão geral](../master-data-services/master-data-services-overview-mds.md) para obter descrições breves de recursos importantes do MDS.  
  
 Consulte [limpeza e correspondência de dados mestres usando](https://msdn.microsoft.com/library/hh403491.aspx) os White papers de EIM Technologies para obter uma orientação abrangente sobre como implementar uma solução de EIM usando essas tecnologias de EIM da Microsoft e assistir ao [EIM (gerenciamento de informações da empresa): reunindo o SSIS, o DQS e o MDS](https://go.microsoft.com/fwlink/?LinkId=258672) video para uma demonstração fria de um cenário de EIM.  
  
 Neste tutorial, você aprenderá a usar o SSIS, o MDS e o DQS em conjunto para implementar um exemplo de solução de Gerenciamento de informações da empresa (EIM). Primeiro, use o DQS para criar uma base de dados de conhecimento que contenha informações sobre os dados (metadados), limpar os dados em um arquivo do Excel usando a base de dados de conhecimento, e fazer a correspondência dos dados para identificar e remover duplicatas. Em seguida, use o Suplemento MDS para Excel a fim de carregar os dados limpos e correspondentes no MDS. Depois, automatize todo o processo usando uma solução SSIS. A solução SSIS neste tutorial lê os dados de entrada de um arquivo do Excel, mas você pode estendê-lo para ler de várias fontes, como Oracle, Teradata, DB2 e banco de dados SQL do Azure.  
  
## <a name="prerequisites"></a>Prerequisites  
  
1.  Microsoft SQL Server 2012 com os seguintes componentes instalados.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Consulte o [Guia de instalação do SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) para obter detalhes sobre como instalar o produto.  
  
2.  [Configure o MDS usando o Gerenciador de Configuração do Master Data Services](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     Use o Gerenciador de Configuração para criar e configura um banco de dados do Master Data Services. Depois de criar o banco de dados do MDS, crie um aplicativo Web para o MDS em um site da [http://localhost/MDS](http://localhost/MDS)Web (por exemplo:) e associe o banco de dados do MDS ao aplicativo Web do MDS. Observe que, para criar um aplicativo Web do MDS, você deve ter o IIS instalado no computador. Consulte [requisitos do aplicativo Web (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx) e [requisitos de banco de dados (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) para obter detalhes sobre os pré-requisitos para configurar o banco de dados MDS e o aplicativo Web.  
  
3.  [Instale e configure o DQS usando o instalador do Data Quality Server](https://msdn.microsoft.com/library/hh231682.aspx). Clique **em Iniciar**, **em todos os programas**, em **Microsoft SQL Server 2014**, em **Data Quality Services**e em **instalador do Data Quality Server**.  
  
4.  Microsoft Excel 2010 (32 bits é preferencial).  
  
5.  Instale o **suplemento do Master Data Services para Excel** (32 bits ou 64-bit com base na versão do Excel que você tem em seu computador) [aqui](https://www.microsoft.com/download/details.aspx?id=29064). Para localizar a versão do Excel instalada no seu computador, execute o **Excel**, clique em **arquivo** na barra de menus e clique em **ajuda** para ver a versão no painel direito. Observe que você precisa instalar o Visual Studio 2010 Tools for Office runtime antes de instalar o Suplemento do Excel.  
  
6.  Adicional Crie uma conta com o [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/). Uma das tarefas no tutorial exige que você tenha uma conta **do Azure Marketplace** (originalmente nomeada **no mercado de dados**). Você poderá ignorar essa tarefa se desejar e passar para a próxima tarefa.  
  
7.  Baixe o arquivo suppliers. xls do [centro de download da Microsoft](https://www.microsoft.com/download/details.aspx?id=50426).  
  
8.  O DQS não permite exportar os resultados de limpeza ou correspondência para um arquivo do Excel se você estiver usando **a versão de 64 bits do Excel**. Esse é um problema conhecido. Para resolvê-lo, faça o seguinte:  
  
    1.  Execute **DQLInstaller. exe-upgrade**. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Clique duas vezes no arquivo DQSInstaller.exe.  
  
    2.  Em **Gerenciador de configuração do Master Data Services**, clique em **Selecionar Banco de dados**, selecione banco de dados **MDS** existente e clique em **Atualizar**.  
  
## <a name="lessons"></a>Lições  
  
|Lição|Breve descrição|Tempo estimado para concluir (em minutos).|  
|------------|-----------------------|------------------------------------------------|  
|[Lição 1: Criando a base de dados de conhecimento do DQS de fornecedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|Nesta lição, você criará uma base de dados de conhecimento do DQS chamada **suppliers**.|60|  
|[Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|Nesta lição, você criará e executará um projeto do DQS para limpar os dados do fornecedor em um arquivo do Excel usando a base de dados de conhecimento dos **fornecedores** criada na primeira lição.|45|  
|[Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|Nesta lição, você criará um projeto do DQS para executar a atividade de correspondência a fim de identificar e remover duplicatas da lista de fornecedores limpa.|45|  
|[Lição 4: Armazenando dados do fornecedor no MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|Nesta lição, você carregará os dados de fornecedor limpos e correspondidos para Master Data Services (MDS) usando o **suplemento MDS para Excel**.|45|  
|[Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|Nesta lição, você criará uma solução SSIS que limpa os dados de entrada usando o DQS, faz a correspondência dos dados limpos para remover duplicatas, e armazena os dados limpos e correspondentes no MDS de forma automatizada.|75|  
  
## <a name="next-steps"></a>Próximas etapas  
 Para iniciar o tutorial, continue na primeira lição: [lição 1: criando a base de dados de conhecimento do DQS dos fornecedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
