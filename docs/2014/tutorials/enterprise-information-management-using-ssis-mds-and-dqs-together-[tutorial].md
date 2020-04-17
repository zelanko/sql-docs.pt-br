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
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487715"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Gerenciamento de informações da empresa usando o SSIS, o MDS e o DQS em conjunto [Tutorial]
  O gerenciamento de informações em uma empresa normalmente envolve a integração dos dados na empresa e fora dela, a limpeza dos dados, a correspondência dos dados para remover qualquer duplicata, a padronização dos dados, o enriquecimento dos dados, a adequação dos dados com os requisitos legais e de conformidade e o armazenamento do dados em um local centralizado com todas as configurações de segurança necessárias.  
  
 O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] fornece todos os componentes necessários para uma solução efetiva de Gerenciamento de Informações da Empresa (EIM) em um único produto. Estes são os principais componentes que ajudam a criar uma solução EIM:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 O SQL Server Integration Services (SSIS) fornece uma plataforma sofisticada e extensível para a integração de dados de várias fontes em uma solução de extração, transformação e carregamento (ETL) abrangente que oferece suporte a fluxos de trabalho comerciais, data warehouse ou gerenciamento de dados mestre. Consulte o tópico [Visão geral dos Serviços de Integração](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) para uma visão geral rápida e usos típicos do SSIS.  
  
 O SQL Server Data Quality Services (DQS) permite a limpeza, a correspondência, a padronização e o enriquecimento dos dados; portanto, é possível enviar informações confiáveis para business intelligence, data warehouse e cargas de trabalho de processamento de transações. Consulte O tópico [Introdução de Serviços de Qualidade de Dados](https://msdn.microsoft.com/library/ff877917.aspx) para a necessidade de DQS e como o DQS responde à necessidade.  
  
 O SQL Server Master Data Services (MDS) fornece um hub de dados central que assegura a constante integridade das informações e consistência dos dados entre diferentes aplicativos. Consulte o tópico [Visão geral dos Serviços de Dados Mestres](../master-data-services/master-data-services-overview-mds.md) para breves descrições de características importantes do MDS.  
  
 Consulte [Limpeza e correspondência de dados mestres usando whitepapers da EIM Technologies](https://msdn.microsoft.com/library/hh403491.aspx) para obter uma orientação abrangente sobre a implementação de uma solução EIM usando essas tecnologias Microsoft EIM em conjunto e assista [ao Enterprise Information Management (EIM): Reunindo vídeos SSIS, DQS e MDS](https://go.microsoft.com/fwlink/?LinkId=258672) para uma demonstração legal de um cenário EIM.  
  
 Neste tutorial, você aprenderá a usar o SSIS, o MDS e o DQS em conjunto para implementar um exemplo de solução de Gerenciamento de informações da empresa (EIM). Primeiro, use o DQS para criar uma base de dados de conhecimento que contenha informações sobre os dados (metadados), limpar os dados em um arquivo do Excel usando a base de dados de conhecimento, e fazer a correspondência dos dados para identificar e remover duplicatas. Em seguida, use o Suplemento MDS para Excel a fim de carregar os dados limpos e correspondentes no MDS. Depois, automatize todo o processo usando uma solução SSIS. A solução SSIS neste tutorial lê os dados de entrada de um arquivo Excel, mas você pode ampliá-los para ler de várias fontes, como Oracle, Teradata, DB2 e Azure SQL Database.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
1.  Microsoft SQL Server 2012 com os seguintes componentes instalados.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Consulte [o Guia de Instalação do SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) para obter detalhes sobre a instalação do produto.  
  
2.  [Configure o MDS usando o Gerenciador de Configuração do Master Data Services](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     Use o Gerenciador de Configuração para criar e configura um banco de dados do Master Data Services. Depois de criar o banco de dados MDS, crie um aplicativo `http://localhost/MDS`web para MDS em um site (por exemplo: ) e associe o banco de dados MDS com o aplicativo web MDS. Observe que, para criar um aplicativo Web do MDS, você deve ter o IIS instalado no computador. Consulte [os Requisitos de Aplicação da Web (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx) e [os Requisitos de Banco de Dados (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) para obter detalhes sobre os pré-requisitos para configurar o banco de dados MDS e o aplicativo web.  
  
3.  [Instale e configure o DQS usando o Instalador do Servidor de Qualidade de Dados](https://msdn.microsoft.com/library/hh231682.aspx). Clique **em Iniciar,** clique em **Todos os programas,** clique no **Microsoft SQL Server 2014,** clique em **Data Quality Services**e clique em Data Quality Server **Installer**.  
  
4.  Microsoft Excel 2010 (32 bits é preferencial).  
  
5.  Instale **o Complemento de Serviços de Dados Mestres para excel** (32 bits ou 64 bits com base na versão do Excel que você tem no seu computador) a partir [daqui](https://www.microsoft.com/download/details.aspx?id=29064). Para encontrar a versão do Excel instalada no seu computador, execute **o Excel**, clique em **Arquivo** na barra de menu e clique em **Ajudar** para ver a versão no painel direito. Observe que você precisa instalar o Visual Studio 2010 Tools for Office runtime antes de instalar o Suplemento do Excel.  
  
6.  (Opcional) Crie uma conta [no Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/). Uma das tarefas no tutorial exige que você tenha uma conta **do Azure Marketplace** (originalmente chamada **de Data Market).** Você poderá ignorar essa tarefa se desejar e passar para a próxima tarefa.  
  
7.  Baixe o arquivo Suppliers.xls do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50426).  
  
8.  O DQS não permite exportar os resultados de limpeza ou correspondência para um arquivo Excel se você estiver usando **a versão de 64 bits do Excel**. Esse é um problema conhecido. Para resolvê-lo, faça o seguinte:  
  
    1.  Executar **dqlinstaller.exe -upgrade**. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Clique duas vezes no arquivo DQSInstaller.exe.  
  
    2.  No **Master Data Services Configuration Manager**, clique em Selecionar banco de **dados,** selecione o banco de dados **MDS** existente e clique em **Atualizar**.  
  
## <a name="lessons"></a>Lições  
  
|Lição|Breve descrição|Tempo estimado para concluir (em minutos).|  
|------------|-----------------------|------------------------------------------------|  
|[Lição 1: Criando a base de dados de conhecimento do DQS de fornecedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|Nesta lição, você cria uma base de conhecimento DQS chamada **Fornecedores**.|60|  
|[Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|Nesta lição, você cria e executa um projeto DQS para limpar os dados do fornecedor em um arquivo Excel usando a Base de Conhecimento **de Fornecedores** que você criou na primeira aula.|45|  
|[Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|Nesta lição, você criará um projeto do DQS para executar a atividade de correspondência a fim de identificar e remover duplicatas da lista de fornecedores limpa.|45|  
|[Lição 4: Armazenando dados do fornecedor no MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|Nesta lição, você carrega os dados do fornecedor limpos e combinados para o Master Data Services (MDS) usando o **Complemento MDS para Excel**.|45|  
|[Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|Nesta lição, você criará uma solução SSIS que limpa os dados de entrada usando o DQS, faz a correspondência dos dados limpos para remover duplicatas, e armazena os dados limpos e correspondentes no MDS de forma automatizada.|75|  
  
## <a name="next-steps"></a>Próximas etapas  
 Para começar o tutorial, continue para a primeira lição: [Lição 1: Criação da Base de Conhecimento Fornecedores DQS](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
