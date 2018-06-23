---
title: Alterar a caixa de diálogo de configurações (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.process.batchsettingsdialog.f1
ms.assetid: 0041e042-d7ce-48f9-a690-a6dc65471ff3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 57dd66ac41586aa1732d7a3a5aeb915450b7c9f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119812"
---
# <a name="change-settings-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Alterar Configurações (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Alterar Configurações** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para alterar as configurações que governam o processamento de objetos listados na caixa de diálogo **Processo** . É possível exibir a caixa de diálogo **Alterar Configurações** clicando em **Alterar Configurações** na caixa de diálogo **Processar** .  
  
> [!NOTE]  
>  As configurações especificadas nessa caixa de diálogo substituem as configurações herdadas do banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dos objetos listados na caixa de diálogo **Processar** .  
  
## <a name="options"></a>Opções  
 **Opções de processamento**  
 Use essa guia para modificar configurações relacionadas à ordem de processamento, à tabela de write-back e aos objetos afetados para a operação de processamento. A guia contém as seguintes opções:  
  
 **Parallel**  
 Clique para processar os objetos em paralelo.  
  
 **Máximo de tarefas paralelas**  
 Selecione o número máximo de tarefas a serem executadas em paralelo pela operação de processamento ou escolha **Deixar o servidor decidir** para permitir que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecione um número ideal de tarefas paralelas.  
  
 **Sequencial**  
 Clique para processar os objetos sequencialmente.  
  
 **Modo de transação**  
 Escolha o modo de transação usado quando os objetos são processados em ordem sequencial:  
  
-   **Uma Transação** processa todos os objetos na mesma transação.  
  
-   **Separar Transações** processa todos os objetos, inclusive objetos dependentes, em transações separadas.  
  
> [!NOTE]  
>  Essa opção estará habilitada apenas se a opção **Sequencial** estiver selecionada.  
  
 **Opção de tabela de write-back**  
 Escolha a opção usada para gerenciar uma tabela de write-back:  
  
-   **Criar** criará uma tabela de write-back se ela não existir. Ocorrerá um erro se uma tabela write-back já existir.  
  
-   **Criar sempre** cria uma tabela write-back se ela não existir ou substitui a tabela write-back existente se ela já existir.  
  
-   **Usar existente** usará a tabela de write-back existente se ela já existir. Ocorrerá um erro se uma tabela write-back não existir.  
  
 **Objetos afetados pelo processo**  
 Selecione para incluir e processar objetos que dependem de objetos incluídos na operação de processamento.  
  
 **Erros de chave de dimensão**  
 Use essa guia para modificar configurações relacionadas à configuração de erros da operação de processamento. A guia contém as seguintes opções:  
  
 **Usar configuração de erro padrão**  
 Selecione para usar a configuração de erro padrão para objetos na operação de processamento.  
  
 **Usar configuração de erro personalizada**  
 Selecione para definir a configuração de erro para objetos na operação de processamento.  
  
 **Ação de erro de chave**  
 Escolha uma das seguintes ações que ocorrem quando uma nova chave é encontrada durante processamento que não pode ser pesquisado:  
  
-   **Converter em desconhecido** agrega as informações do registro ao membro desconhecido.  
  
-   **Descartar registro** exclui a informações do registro para que não sejam processadas com o objeto.  
  
 **Ignorar contagem de erros**  
 Clique para ignorar quaisquer erros ocorridos durante o processamento.  
  
 **Parar se houver erro**  
 Clique para interromper o processamento quando ocorrerem erros. Essa opção habilita as opções **Número de erros** e **Ação se houver erro** .  
  
 **Número de erros**  
 Digite o número de erros que são ignorados antes do processamento ser encerrado.  
  
 **Ação se houver erro**  
 Escolha uma das seguintes ações a serem executadas quando o número de erros exceder o valor em **Número de erros**:  
  
-   **Parar processamento** encerra a operação de processamento.  
  
-   **Parar log** para o log de erros, mas continua a operação de processamento.  
  
 **Chave não encontrada**  
 Especifique uma das seguintes ações a ser executada quando uma chave não for localizada quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro.  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave duplicada**  
 Especifique uma das seguintes ações a ser executada se uma chave duplicada for localizada quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro.  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave nula convertida em desconhecida**  
 Especifique uma das seguintes ações a ser executada quando uma chave de membro nula for adicionada ao membro desconhecido quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro.  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave nula não permitida**  
 Especifique uma das seguintes ações a ser executada quando uma chave nula for localizada, mas não for permitida, quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro.  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Caminho do log de erros**  
 Digite o caminho completo e nome do arquivo de log de erros.  
  
 **Procurar**  
 Clique para abrir a caixa de diálogo **Abrir** e selecionar o caminho completo e o nome do arquivo de log de erros.  
  
 **Objetos afetados pelo processo**  
 Clique para processar os objetos que têm uma dependência dos objetos selecionados na caixa de diálogo **Processar** .  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Processar a caixa de diálogo &#40;Analysis Services - dados multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  