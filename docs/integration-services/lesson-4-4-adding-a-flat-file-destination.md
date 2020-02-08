---
title: 'Etapa 4: Adicionar um destino de Arquivo Simples | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae02b9188ecc9917d26532633e4d5a253d4f326b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295942"
---
# <a name="lesson-4-4-add-a-flat-file-destination"></a>Lição 4-4: Adicionar um destino de Arquivo Simples

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



A saída de erro da transformação Pesquisar Chave de Moeda redireciona todas as linhas de dados que falharam na pesquisa para a operação de transformação de Script. Para fornecer mais informações sobre os erros que ocorreram, a transformação Script executa um script que contém a descrição de cada erro.  
  
Nesta tarefa, você salva todas essas informações sobre as linhas com falha em um arquivo de texto delimitado, para processamento posterior. Para salvar as linhas com falha, adicione e configure um gerenciador de conexões de arquivo simples para o arquivo de texto que contém os dados de erro e um arquivo simples de destino. Ao definir propriedades no gerenciador de conexões de arquivo simples que o arquivo simples usa, você pode especificar como o destino do arquivo simples formata e escreve o arquivo de texto. Para obter mais informações, confira [Gerenciador de conexões de Arquivo Simples](../integration-services/connection-manager/flat-file-connection-manager.md) e [Destino de Arquivo Simples](../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="add-and-configure-a-flat-file-destination"></a>Adicionar e configurar um destino de arquivo simples  
  
1.  Selecione a guia **Fluxo de Dados**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outros Destinos** e arraste **Destino de Arquivo Simples** para a superfície de design de fluxo de dados. Coloque **Destino de Arquivo Simples** diretamente embaixo da transformação **Obter Descrição do Erro** .  
  
3.  Selecione a transformação **Obter Descrição do Erro** e arraste a seta azul sobre o novo **Destino de Arquivo Simples**.  
  
4.  Na superfície de design de **Fluxo de Dados**, selecione o nome **Destino de Arquivo Simples** na nova transformação **Destino de Arquivo Simples** e altere o nome para **Linhas com Falha**.  
  
5.  Clique com o botão direito do mouse na transformação **Linhas com Falha**, selecione **Editar** e, no **Editor de Destino de Arquivo Simples**, selecione **Novo**.  
  
6.  Na caixa de diálogo **Formato de Arquivo Simples**, verifique se **Delimitado** está selecionado e depois selecione **OK**.  
  
7.  No **Editor do Gerenciador de Conexões de Arquivo Simples**, no tipo de caixa **Nome do Gerenciador de Conexões** insira *Dados do Erro*.  
  
8.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, selecione **Procurar** e localize a pasta em que o arquivo será armazenado.  
  
9. Na caixa de diálogo **Abrir**, para **Nome do arquivo**, insira *ErrorOutput.txt* e selecione **Abrir**.  
  
10. Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, verifique se **Localidade** é **Inglês (Estados Unidos)** e se **Página de código** é **1252 (ANSI-Latino I)** .  
  
11. No painel de opções, selecione **Colunas**.  
  
    Além das colunas do arquivo de dados de origem, há três colunas novas: ErrorCode, ErrorColumn e ErrorDescription. Essas colunas são a saída de erro da transformação Pesquisar Chave de Moeda e o script na transformação Obter Descrição do Erro. Você pode usar essas colunas para solucionar problemas e detectar a causa da linha com falha.  
  
12. Selecione **OK**.  
  
13. No **Editor de Destino de Arquivo Simples**, desmarque a caixa de seleção **Substituir dados no arquivo** .  
  
    Desmarcar essa caixa de seleção persiste os erros em várias execuções de pacote acrescentando a saída de erro de cada nova execução.
  
14. No **Editor de Destino de Arquivo Simples**, selecione **Mapeamentos** para verificar se todas as colunas estão corretas. Como alternativa, você pode renomear as colunas no destino.  
  
15. Selecione **OK**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 5: Testar o pacote de tutorial da Lição 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  
