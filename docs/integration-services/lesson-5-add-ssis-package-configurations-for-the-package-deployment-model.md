---
title: "Lição 5: Adicionar configurações de pacote do SSIS para o modelo de implantação do pacote | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a16217f90b9120993663d9046c8178e62451111
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>Lição 5: Adicionar configurações do pacote SSIS ao modelo de implantação de pacotes
As configurações de pacote deixam você definir propriedades de tempo de execução e variáveis de fora do ambiente de desenvolvimento. As configurações permitem que você desenvolva pacotes que flexíveis e fáceis de implantar e distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece os seguintes tipos de configuração:  
  
-   Arquivo de configuração XML  
  
-   Variável de ambiente  
  
-   Entrada de Registro  
  
-   Variável de pacote pai  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] table  
  
Nesta lição, você aprenderá a modificar o pacote simples do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] criado na [Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) para usar o Modelo de Implantação de Pacote e aproveitar as configurações do pacote. Você também pode copiar o pacote concluído da Lição 4 que está incluso no tutorial. Usando o Assistente de Configuração de Pacote, você criará uma configuração XML que atualiza a propriedade **Directory** do contêiner Loop Foreach usando uma variável em nível de pacote mapeada para a propriedade Directory. Depois de criar um arquivo de configuração, você modificará o valor da variável de fora do ambiente de desenvolvimento e apontará a propriedade modificada para uma nova pasta de dados de exemplo. Quando você executa o pacote novamente, o arquivo de configuração popula o valor da variável e a variável, por sua vez, atualiza a propriedade **Directory**. Como resultado, o pacote itera através dos arquivos na nova pasta de dados, em vez de iterar através de arquivos na pasta original que foi codificada no pacote.  
  
> [!IMPORTANT]  
> Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Reporting Services Product Samples on CodePlex (Amostras de produto do Reporting Services no CodePlex)](http://go.microsoft.com/fwlink/p/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da lição 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Etapa 2: Habilitar e configurar as configurações de pacote](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Etapa 3: Modificando o valor de configuração de propriedade de diretório](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Etapa 4: Testando o pacote de Tutorial da lição 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
  
-   [Etapa 1: Copiando o pacote da lição 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  

