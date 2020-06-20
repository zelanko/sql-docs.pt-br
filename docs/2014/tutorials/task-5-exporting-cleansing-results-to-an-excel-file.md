---
title: 'Tarefa 5: exportando resultados de limpeza para um arquivo do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 44c926d2429a0d9842e9e9202568f73f72c89d9a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064745"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Tarefa 5: Exportando os resultados da limpeza para um arquivo do Excel
  Nesta tarefa, você exportará resultados da atividade de limpeza para um arquivo do Excel. Confira o tópico [Exportar estágio](https://msdn.microsoft.com/library/hh213061.aspx#Export) para obter mais detalhes.  
  
1.  No painel direito, selecione **Excel** para o **tipo de destino**.  
  
2.  Clique em **procurar**, especifique o nome do arquivo de saída como **fornecedor limpo List.xls**e clique em **abrir**.  
  
3.  Selecione **dados somente** para o formato de **saída** para exportar apenas os dados limpos. A segunda opção, **dados e informações de limpeza**, permitem exportar detalhes da atividade de limpeza junto com os dados limpos. A opção **padronizar formato** permite aplicar qualquer formato de saída definido em um domínio aos valores desse domínio. Você não definiu um formato de saída em nenhum domínio no tutorial.  
  
     ![Página Exportar Resultados da Limpeza](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "Página Exportar Resultados da Limpeza")  
  
4.  Clique em **Exportar** para exportar os dados. Não clique em **concluir** ainda.  
  
5.  Clique em **fechar** na caixa de diálogo **Exportar** .  
  
6.  Clique em **concluir** para concluir a atividade. Se você se esqueceu de exportar os resultados antes de clicar em **concluir**, clique em **Abrir projeto de qualidade de dados** na página principal do cliente do **DQS**, selecione **Limpar lista de fornecedores** na lista de projetos e clique em **Avançar** na parte inferior da tela para obter o estágio de **exportação** do processo de limpeza novamente. Você também pode alternar para a guia **gerenciar e exibir resultados** clicando no botão **voltar** .  
  
7.  Abra o **List.xlsdo fornecedor limpo** e faça o seguinte:  
  
    1.  Verifique se não há endereços de email que terminem com adventure-work.com (sem o caractere ') procurando por adventure-work.com na planilha.  
  
    2.  Veja que não há nenhum valor **usa** na coluna **Country** .  
  
    3.  Procure **Los Angeles** e verifique se o **State** está definido como **CA**.  
  
    4.  Confirme que não há termos **co.**, **Corp.**, e **Inc.**.  
  
    5.  Exclua a coluna **validação de endereço** da planilha e salve o arquivo do Excel. Essa coluna adicional corresponde ao domínio composto Address Validation.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Importando valores do projeto Limpar Lista de Fornecedores](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
