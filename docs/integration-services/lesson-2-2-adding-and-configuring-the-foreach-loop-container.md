---
title: 'Etapa 2: Adicionar e configurar o contêiner Loop Foreach | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c865c00eb1020aa6128cdd7a40d61a191bad2a3
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722737"
---
# <a name="lesson-2-2-add-and-configure-the-foreach-loop-container"></a>Lição 2-2: Adicionar e configurar o contêiner Loop Foreach

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nessa tarefa, você adicionará a capacidade de executar loop através de uma pasta de arquivos simples e aplicará a transformação de fluxo de dados da Lição 1 a cada um desses arquivos simples. Você faz isto adicionando e configurando um contêiner Loop Foreach ao fluxo de controle.  
  
O contêiner Loop Foreach que você adicionar deve ser capaz de se conectar a cada arquivo simples na pasta. Como todos os arquivos da pasta têm o mesmo formato, o contêiner Loop Foreach pode usar o mesmo gerenciador de conexões de Arquivo Simples para conectar-se a cada um desses arquivos. O gerenciador de conexão do Arquivo Simples que o contêiner usa é o que você criou na Lição 1.  
  
Atualmente, o gerenciador de conexões de Arquivo Simples da Lição 1 se conecta a um único arquivo simples específico. Para conectar-se iterativamente a cada arquivo simples da pasta, é preciso configurar o contêiner Loop Foreach e o gerenciador de conexões de Arquivo Simples da seguinte maneira:  
  
-   **Contêiner do Loop Foreach:** Mapeie o valor enumerado do contêiner para uma variável de pacote definida pelo usuário. O contêiner usará essa variável para modificar dinamicamente a propriedade **ConnectionString** do gerenciador de conexões de Arquivo Simples e conectar-se de forma iterativa a cada um dos arquivos simples da pasta.  
  
-   **Gerenciador de conexões de Arquivo Simples:** Modifique o gerenciador de conexões criado na Lição 1 usando uma variável definida pelo usuário para popular a propriedade **ConnectionString** do gerenciador de conexões.  
  
Os procedimentos nessa tarefa mostram como você pode criar e modificar o contêiner Loop Foreach para usar uma variável definida pelo usuário e adicionar a tarefa de fluxo de dados ao loop. Você aprenderá como modificar o gerenciador de conexões de Arquivo Simples para usar a variável definida pelo usuário na próxima tarefa.  
  
Após essas modificações no pacote, quando ele for executado, o contêiner Loop Foreach iterará através de todos os arquivos na pasta Dados de Exemplo. Sempre que um arquivo que corresponda aos critérios for encontrado, o contêiner Loop Foreach preencherá a nova variável com o nome do arquivo, mapeará essa variável para a propriedade **ConnectionString** do gerenciador de conexões de Arquivo Simples dos Dados de Moeda de Exemplo e executará o fluxo de dados nesse arquivo. Dessa forma, em cada iteração do Loop Foreach a tarefa de Fluxo de Dados consumirá um arquivo simples diferente.  
  
> [!NOTE]  
> Como o [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de controle do fluxo de dados, qualquer loop que você adicionar ao fluxo de controle não exigirá modificações no fluxo de dados. Portanto, o fluxo de dados da Lição 1 não precisará ser alterado.  
  
## <a name="add-a-foreach-loop-container"></a>Adicionar um contêiner Loop Foreach  
  
1.  No **SQL Server Data Tools**, selecione a guia **Fluxo de Controle**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Contêineres**e arraste um **Contêiner Loop Foreach** até a superfície de design da guia **Fluxo de Controle** .  
  
3.  Clique com o botão direito do mouse no novo **Contêiner Loop Foreach** e selecione **Editar**.  
  
4.  Na caixa de diálogo **Editor de Loop Foreach**, na página **Geral**, em **Nome**, insira **Arquivo Foreach na Pasta**. Escolha **OK**.  
  
5.  Clique com o botão direito do mouse no contêiner Loop Foreach, selecione **Propriedades** e, na janela **Propriedades**, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)**.  
  
## <a name="configure-the-enumerator-for-the-foreach-loop-container"></a>Configurar o enumerador para o contêiner Loop Foreach  
  
1.  Clique duas vezes em **Arquivo Foreach na Pasta** para abrir novamente o **Editor de Loop Foreach**.  
  
2.  Selecione **Coleção**.  
  
3.  Na página **Coleção** , selecione **Enumerador de Arquivo Foreach**.  
  
4.  No grupo **Configuração do enumerador**, selecione **Procurar**.  
  
5.  Na caixa de diálogo **Procurar pasta**, localize a pasta no computador que contém os arquivos Currency_*.txt incluídos nos dados de exemplo.

6.  Na caixa **Arquivos**, digite **Currency_\*.txt**.  
  
## <a name="map-the-enumerator-to-a-user-defined-variable"></a>Mapear o enumerador para uma variável definida pelo usuário  
  
1.  Selecione **Mapeamentos de Variáveis**.  
  
2.  Na página **Mapeamentos de Variáveis**, na coluna **Variável**, selecione a célula vazia e selecione **\<Nova Variável...>**.  
  
3.  Na caixa de diálogo **Adicionar Variável**, em **Nome**, digite **varFileName**.  
  
    > [!NOTE]  
    > Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
4.  Escolha **OK**.  
  
5.  Selecione **OK** novamente para sair da caixa de diálogo **Editor de Loop Foreach**.  
  
## <a name="add-the-data-flow-task-to-the-loop"></a>Adicionar a tarefa de fluxo de dados ao loop  
  
-   Arraste a tarefa de fluxo de dados **Extrair Dados de Moeda de Exemplo** até o contêiner Loop Foreach **Arquivo Foreach na Pasta**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 3: Modificar o gerenciador de conexões de Arquivo Simples](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Confira também  
[Configurar um contêiner Loop Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
