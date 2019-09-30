---
title: 'Lição 2: Adicionar looping com o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ccd3be3203aae382cda239ed6d7bdc2fa224923b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296060"
---
# <a name="lesson-2-add-looping-with-ssis"></a>Lição 2: Adicionar looping com o SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Na [Lição 1: Criar um projeto e pacote básico com o SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md), você criou um pacote que extrai dados de uma fonte de arquivo simples. Os dados então são transformados usando transformações de Pesquisa. Por fim, o pacote carrega os dados para uma cópia da tabela de fatos **FactCurrencyRate** no banco de dados de amostra **AdventureWorksDW2012**.  
  
Um processo de ETL (extração, transformação e carregamento) normalmente extrai dados de várias fontes de arquivo simples. Extrair dados de várias fontes requer um fluxo de controle iterativo. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pode facilmente adicionar iterações ou loops aos pacotes.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece dois tipos de contêineres para efetuar loop por meio de pacotes: Foreach Loop e Loop For. O contêiner Foreach Loop usa um enumerador para o loop, enquanto que o contêiner For Loop geralmente usa uma expressão de variável. Esta lição usa o contêiner Loop Foreach.  
  
O contêiner Loop Foreach habilita um pacote a repetir o fluxo de controle para cada membro de um enumerador especificado. Com o contêiner Loop Foreach, você pode enumerar:  
  
-   Linhas do conjunto de registros ADO  
  
-   Informações de esquema do ADO .Net  
  
-   Estruturas de arquivo e diretório  
  
-   Variáveis de sistema, pacote e usuário  
  
-   Objetos enumeráveis em uma variável  
  
-   Itens de uma coleção  
  
-   Nós em uma expressão XML Path Language (XPath)  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SMO (Management Objects)  
  
Nesta lição, você modifica o pacote ETL de exemplo da Lição 1 para usar um contêiner Foreach Loop e define uma variável de pacote definida pelo usuário para o pacote. Essa variável então é usada para iterar os arquivos correspondentes na pasta de exemplo.   
  
Nesta lição, você não modificará o fluxo de dados, apenas o fluxo de controle.  
  
> [!NOTE]  
> Se você ainda não fez isso, confira a [Lição 1 Pré-requisitos](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [Etapa 2: Adicionar e configurar o contêiner Loop Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [Etapa 3: Modificar o gerenciador de conexões de Arquivo Simples](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [Etapa 4: Testar o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiar o pacote da Lição 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>Confira também  
[Contêiner do Loop For](../integration-services/control-flow/for-loop-container.md)  
  
  
  
