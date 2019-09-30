---
title: SSIS – Como criar um pacote ETL | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9a36d403867699a02adfec0d04c9db4efa803514
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281887"
---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS: Como criar um pacote ETL

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Neste tutorial, você aprenderá a usar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para criar um pacote simples do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. O pacote que você cria conduz dados de um arquivo simples, formata esses dados e insere os dados formatados em uma tabela de fatos. Nas lições a seguir, o pacote é expandido para demonstrar looping, configurações de pacote, registro de log e fluxo de erros.  
  
Ao instalar os dados de exemplo usados pelo tutorial, as versões concluídas dos pacotes criados para cada lição do tutorial também são instaladas. Ao utilizar os pacotes concluídos, será possível começar o tutorial em uma lição posterior, caso queira. Se este tutorial for a primeira vez que você trabalha com pacotes ou com o novo ambiente de desenvolvimento, recomendamos que você comece pela lição 1.  

## <a name="what-is-sql-server-integration-services-ssis"></a>O que é o SSIS (SQL Server Integration Services)?

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] O SSIS é uma plataforma para a criação de soluções de integração de dados de alto desempenho, incluindo os pacotes ETL (extração, transformação e carregamento) para armazenamento de dados. O SSIS inclui ferramentas gráficas e assistentes para criação e depuração de pacotes; tarefas para execução de funções de fluxo de trabalho como, por exemplo, operações de FTP, execução de instruções SQL e envio de mensagens de email; fontes de dados e destinos para extração e carregamento de dados; transformações para limpeza, agregação, junção e cópia de dados; um serviço de gerenciamento, `SSISDB`, para administração de execução e armazenamento de pacotes; e APIs (interfaces de programação de aplicativo) para programação do modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  

## <a name="what-you-learn"></a>O que você aprenderá  
O melhor modo de se familiarizar com as novas ferramentas, controles e recursos disponíveis no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é utilizando-os. Este tutorial explicará como usar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para criar um pacote de ETL simples com looping, configurações, lógica de fluxo de erros e registro de logs.  
  
## <a name="prerequisites"></a>Prerequisites  
O tutorial é destinado a usuários familiarizados com operações básicas de banco de dados, mas que tiveram pouca experiência com os novos recursos disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  

Para executar esse tutorial, os seguintes componentes devem estar instalados:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para instalar o SQL Server e o SSIS, consulte [Instalar o Integration Services](install-windows/install-integration-services.md).

-   O banco de dados de exemplo **AdventureWorksDW2012**. Para baixar o banco de dados **AdventureWorksDW2012**, baixe `AdventureWorksDW2012.bak` em [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e restaure o backup.  

-   Os arquivos de **dados de exemplo**. Os dados de exemplo estão incluídos com os pacotes de lição do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para baixar os dados de exemplo e os pacotes de lição como um arquivo zip, veja os [Arquivos de Tutorial do SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827).

    - A maioria dos arquivos no arquivo Zip é somente leitura a fim de impedir alterações acidentais. Para gravar algo em um arquivo ou alterá-lo, talvez você precise desligar o atributo somente leitura nas propriedades do arquivo.
    - Os pacotes de exemplo pressupõem que os arquivos de dados estão na pasta `C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Creating a Simple ETL Package`. Se você descompactar o download em outro local, talvez precise atualizar o caminho do arquivo em vários locais nos pacotes de exemplo.

## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
[Lição 1: criar um projeto e pacote básico com o SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
Nesta lição, você criará um pacote ETL simples que extrairá dados de um único arquivo simples, transformará os dados usando transformações de pesquisa e, por fim, carregará o resultado em um destino da tabela de fatos.  
  
[Lição 2: adicionar um loop com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na Lição 1 para aproveitar os novos recursos de looping para extrair vários arquivos simples em um único processo de fluxo de dados.  
  
[Lição 3: adicionar registro em log com o SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 2 para aproveitar os novos recursos de registro de log.  
  
[Lição 4: adicionar o redirecionamento de fluxo de erro com o SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 3 para aproveitar as novas configurações de saída de erro.  
  
[Lição 5: adicionar configurações do pacote SSIS ao Modelo de Implantação de Pacotes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
Nesta lição, você expandirá o pacote criado na lição 4 para aproveitar as novas opções de configuração de pacote.  
  
[Lição 6: usar parâmetros com o modelo de implantação de projetos no SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
Nesta lição, você expandirá o pacote criado na lição 5 para usar os novos parâmetros com o modelo de implantação de projeto.  
  
  
  
