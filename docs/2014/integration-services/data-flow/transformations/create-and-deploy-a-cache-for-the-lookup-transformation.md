---
title: Criar e implantar um cache para a transformação Pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef5450bc9598f86909bbb032adcfa4bfc0fc9040
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381064"
---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>Criar e implantar um cache para a Transformação Pesquisa
  Você pode criar e implementar um arquivo de cache (.caw) para uma transformação Pesquisa. O conjunto de dados de referência é armazenado no arquivo de cache.  
  
 A transformação Pesquisa executa pesquisas ao unir dados em colunas de dados de uma fonte de dados conectados com colunas no conjunto de dados de referência.  
  
 Você cria um arquivo de cache usando um gerenciador de conexões de cache e uma transformação Cache. Para obter mais informações, consulte [Editor do Gerenciador de Conexões de Cache](../../connection-manager/cache-connection-manager.md) e [Transformação de Cache](cache-transform.md).  
  
 Para saber mais sobre a transformação Pesquisa e os arquivos de cache, consulte [Transformação Pesquisa](lookup-transformation.md).  
  
### <a name="to-create-a-cache-file"></a>Para criar um arquivo de cache  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja, e, então, abra o pacote.  
  
2.  Na guia **Fluxo de Controle** , adicione uma tarefa de Fluxo de Dados.  
  
3.  Na guia **Fluxo de Dados** , adicione uma transformação Cache Transform ao fluxo de dados, e, então, conecte a transformação à fonte de dados.  
  
     Configure a fonte de dados como necessário.  
  
4.  Clique duas vezes na transformação Cache e, depois, em **Editor de Transformação Cache**, na página **Gerenciador de Conexões** , clique em **Novo** para criar um novo gerenciador de conexões de Cache.  
  
5.  No **Editor do Gerenciador de Conexões de Cache**, na guia **Geral** , configure o gerenciador de conexões de cache para salvar o cache selecionando as seguintes opções:  
  
    1.  Selecione **Usar Cache de Arquivo**.  
  
    2.  Para **Nome do arquivo**, digite o caminho de arquivo.  
  
     O sistema cria o arquivo quando você executa o pacote.  
  
    > [!NOTE]  
    >  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../access-to-files-used-by-packages.md).  
  
6.  Clique na guia **Colunas** e, então, especifique quais são as colunas de índice usando a opção **Posição do Índice** .  
  
     Para colunas sem-índice, a posição de índice é 0. Para colunas de índice, a posição de índice é um número sequencial positivo.  
  
    > [!NOTE]  
    >  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas.  
  
     Para obter mais informações, consulte [Cache Connection Manager Editor](../../cache-connection-manager-editor.md).  
  
7.  Configure o Cache Transform como necessário.  
  
     Para obter mais informações, consulte [Editor de Transformação Cache &#40;Página Gerenciador de Conexões&#41;](../../cache-transformation-editor-connection-manager-page.md) e [Editor de Transformação Cache &#40;Página Mapeamentos&#41;](../../cache-transformation-editor-mappings-page.md).  
  
8.  Execute o pacote.  
  
### <a name="to-deploy-a-cache-file"></a>Para implementar um arquivo de cache  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja, e, então, abra o pacote.  
  
2.  Opcionalmente, crie uma configuração de pacote Para obter mais informações, consulte [Criar configurações de pacote](../../create-package-configurations.md).  
  
3.  Adicione o arquivo de cache ao projeto fazendo o seguinte:  
  
    1.  No Gerenciador de Soluções, selecione o projeto que você abriu na etapa 1.  
  
    2.  No menu **Projeto** , clique em **Item AddExisting**.  
  
    3.  Selecione o arquivo de cache e clique em **Adicionar**.  
  
     O arquivo aparece na pasta **Diversos** no Gerenciador de Soluções.  
  
4.  Configure o projeto para criar um utilitário de implantação e, em seguida, crie o projeto. Para obter mais informações, consulte [Criar um utilitário de implantação](../../create-a-deployment-utility.md).  
  
     Um arquivo de manifesto, \<*nome do projeto*>.SSISDeploymentManifest.xml é criado e lista os arquivos diversos no projeto, os pacotes e as configurações de pacote.  
  
5.  Implemente os pacotes no sistema de arquivos Para obter mais informações, consulte [Implantar pacotes por meio do utilitário de implantação](../../deploy-packages-by-using-the-deployment-utility.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um utilitário de implantação](../../create-a-deployment-utility.md)  
  
  
