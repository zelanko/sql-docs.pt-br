---
title: 'Lição 5: adicionando configurações de pacote para o modelo de implantação de pacote | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d454b5b064068d95a97e96bf7e4767455eb5f19d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951531"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>Lição 5: Como adicionar configurações de pacote para o modelo de implantação de pacote
  As configurações de pacote deixam você definir propriedades de tempo de execução e variáveis de fora do ambiente de desenvolvimento. As configurações permitem que você desenvolva pacotes que flexíveis e fáceis de implantar e distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece os seguintes tipos de configuração:  
  
-   Arquivo de configuração XML  
  
-   Variável de ambiente  
  
-   Entrada de Registro  
  
-   Variável de pacote pai  
  
-   Tabela [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 Nesta lição, você modificará o pacote simples do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] criados na [Lesson 4: Adding Error Flow Redirection](lesson-4-add-error-flow-redirection-with-ssis.md) para usar o Modelo de Implantação de Pacote e aproveitar as configurações do pacote. Você também pode copiar o pacote concluído da Lição 4 que está incluso no tutorial. Usando o Assistente de Configuração de Pacote, você irá criar uma configuração XML que atualiza a propriedade `Directory` do contêiner Loop Foreach utilizando uma variável de nível de pacote mapeada para a propriedade do Diretório. Depois de criar um arquivo de configuração, você modificará o valor da variável de fora do ambiente de desenvolvimento e apontará a propriedade modificada para uma nova pasta de dados de exemplo. Quando você executa o pacote novamente, o arquivo de configuração popula o valor da variável e a variável, por sua vez, atualiza a `Directory` propriedade. Como resultado, o pacote itera através dos arquivos na nova pasta de dados, em vez de iterar através de arquivos na pasta original que foi codificada no pacote.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Amostras de produto do Reporting Services no CodePlex](https://go.microsoft.com/fwlink/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Etapa 2: Habilitar e configurar configurações de pacote](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Etapa 3: Modificar o valor de configuração da propriedade de diretório](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Etapa 4: Testar o pacote de tutorial da Lição 5](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
  
-   [Etapa 1: Copiar o pacote da Lição 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
