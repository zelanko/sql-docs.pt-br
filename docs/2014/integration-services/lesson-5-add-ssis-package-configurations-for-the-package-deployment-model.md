---
title: 'Lição 5: Adicionando configurações de pacote para o modelo de implantação de pacote | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e2d995b06d30157ae46669696e9f8d4095a4646
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362198"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>Lição 5: Adicionando configurações de pacote para o modelo de implantação de pacote
  As configurações de pacote deixam você definir propriedades de tempo de execução e variáveis de fora do ambiente de desenvolvimento. As configurações permitem que você desenvolva pacotes que flexíveis e fáceis de implantar e distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece os seguintes tipos de configuração:  
  
-   Arquivo de configuração XML  
  
-   Variável de ambiente  
  
-   Entrada de Registro  
  
-   Variável de pacote pai  
  
-   Tabela [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 Nesta lição, você modificará o simples [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pacote que você criou na [lição 4: Adicionando redirecionamento de fluxo de erro](lesson-4-add-error-flow-redirection-with-ssis.md) para usar o modelo de implantação de pacote e aproveitar as configurações do pacote. Você também pode copiar o pacote concluído da Lição 4 que está incluso no tutorial. Usando o Assistente de Configuração de Pacote, você irá criar uma configuração XML que atualiza a propriedade `Directory` do contêiner Loop Foreach utilizando uma variável de nível de pacote mapeada para a propriedade do Diretório. Depois de criar um arquivo de configuração, você modificará o valor da variável de fora do ambiente de desenvolvimento e apontará a propriedade modificada para uma nova pasta de dados de exemplo. Quando você executar o pacote novamente, o arquivo de configuração popula o valor da variável e a variável por sua vez atualiza o `Directory` propriedade. Como resultado, o pacote itera através dos arquivos na nova pasta de dados, em vez de iterar através de arquivos na pasta original que foi codificada no pacote.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Reporting Services Product Samples on CodePlex (Amostras de produto do Reporting Services no CodePlex)](https://go.microsoft.com/fwlink/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da lição 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Etapa 2: Configurando e habilitando configurações de pacote](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Etapa 3: Modificando o valor de configuração de propriedade de diretório](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Etapa 4: Testando o pacote de Tutorial da lição 5](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
  
-   [Etapa 1: Copiando o pacote da lição 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
