---
title: 'Tarefa 5: Exportar resultados da limpeza para um arquivo do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8a716d3b6c0007ceb89f36f23584bb4adb4f706
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007172"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Tarefa 5: Exportando os resultados da limpeza para um arquivo do Excel
  Nesta tarefa, você exportará resultados da atividade de limpeza para um arquivo do Excel. Consulte [estágio de exportação](http://msdn.microsoft.com/library/hh213061.aspx#Export) tópico para obter mais detalhes.  
  
1.  No painel direito, selecione **Excel** para o **tipo de destino**.  
  
2.  Clique em **procurar**, especifique o nome do arquivo de saída como **Cleansed Supplier List.xls**e, em seguida, clique em **abrir**.  
  
3.  Selecione **somente dados** para o **saída** formato para exportar apenas os dados limpos. A segunda opção, **dados e informações de limpeza**, permite exportar detalhes da atividade de limpeza juntamente com os dados limpos. O **padronizar formato** opção permite que você aplique quaisquer formatos de saída definidos em um domínio para os valores desse domínio. Você não definiu um formato de saída em nenhum domínio no tutorial.  
  
     ![Página resultados da limpeza de exportação](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "página resultados da limpeza de exportação")  
  
4.  Clique em **exportar** para exportar os dados. Não clique **concluir** ainda.  
  
5.  Clique em **fechar** no **exportando** caixa de diálogo.  
  
6.  Clique em **concluir** para concluir a atividade. Se você esqueceu de exportar os resultados antes de clicar em **concluir**, clique em **Abrir projeto de qualidade de dados** na página principal do **cliente DQS**, selecione **limpar Supplier Lista** da lista de projetos e clique em **próximo** na parte inferior da tela para obter o **exportar** estágio do processo de limpeza novamente. Você também pode alternar para **gerenciar e exibir resultados** guia clicando **novamente** botão.  
  
7.  Abra o **Cleansed Supplier List.xls** e faça o seguinte:  
  
    1.  Verifique se não há nenhum endereço de email que termine com adventure-work.com (sem o caractere ‘s’) procurando adventure-work.com na planilha.  
  
    2.  Consulte que não há nenhum **EUA** valor no **país** coluna.  
  
    3.  Procurar **Los Angeles** e ver que o **estado** é definido como **CA**.  
  
    4.  Confirme se não há nenhum termos **co.**, **corp.**, e **Inc.**.  
  
    5.  Excluir o **Address Validation** coluna da planilha e salve o arquivo do excel. Essa coluna adicional corresponde ao domínio composto Address Validation.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Importando valores do projeto Limpar Lista de Fornecedores](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  