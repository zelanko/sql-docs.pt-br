---
title: 'Lição 5: Adicionar configurações do pacote SSIS ao Modelo de Implantação de Pacotes | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6246183a4a928e1813125676753c827bf20cf8c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721165"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>Lição 5: Adicionar configurações do pacote SSIS ao Modelo de Implantação de Pacotes

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



As configurações de pacote deixam você definir propriedades de tempo de execução e variáveis de fora do ambiente de desenvolvimento. As configurações permitem que você desenvolva pacotes que flexíveis e fáceis de implantar e distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece os seguintes tipos de configuração:  
  
-   Arquivo de configuração XML  
  
-   Variável de ambiente  
  
-   Entrada de Registro  
  
-   Variável de pacote pai  
  
-   Tabela [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
Nesta lição, você modificará o pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de exemplo criado na [Lição 4: Adicione redirecionamento de fluxo de erro com SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) para usar o Modelo de Implantação de Pacote e aproveitar as configurações do pacote. Você também pode copiar o pacote concluído da Lição 4 incluso no tutorial. 

Usando o Assistente de Configuração de Pacote, você cria uma configuração de XML que atualiza a propriedade **Directory** do contêiner Foreach Loop. Você usa uma variável em nível de pacote mapeada para a propriedade **Directory**. Depois de criar o arquivo de configuração, você pode modificar o valor da variável de fora do ambiente de desenvolvimento para um novo caminho de pasta de dados de exemplo. Quando você executa o pacote novamente, o arquivo de configuração popula o valor da variável e a variável, por sua vez, atualiza a propriedade **Directory** . O pacote então itera pelos arquivos na nova pasta de dados, em vez de na pasta original embutida em código.  
  
> [!NOTE]
> Se você ainda não fez isso, confira os [Pré-requisitos da Lição 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Etapa 2: Habilitar e configurar as configurações do pacote](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Etapa 3: Modificar o valor de configuração da propriedade Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Etapa 4: Testar o pacote da Lição 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
  
-   [Etapa 1: Copiar o pacote da Lição 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
