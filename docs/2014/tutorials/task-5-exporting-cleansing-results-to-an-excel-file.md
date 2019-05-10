---
title: 'Tarefa 5: Exportando os resultados para um arquivo do Excel da limpeza | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489121"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Tarefa 5: Exportar os resultados da limpeza para um arquivo do Excel
  Nesta tarefa, você exportará resultados da atividade de limpeza para um arquivo do Excel. Ver [estágio de exportação](https://msdn.microsoft.com/library/hh213061.aspx#Export) tópico para obter mais detalhes.  
  
1.  No painel direito, selecione **Excel** para o **tipo de destino**.  
  
2.  Clique em **navegue**, especifique o nome do arquivo de saída como **Cleansed Supplier List**e, em seguida, clique em **abrir**.  
  
3.  Selecione **Data Only** para o **saída** formato para exportar apenas os dados limpos. A segunda opção, **dados e informações de limpeza**, permite exportar os detalhes da atividade de limpeza juntamente com os dados limpos. O **padronizar formato** opção permite que você aplique quaisquer formatos de saída definidos em um domínio para os valores desse domínio. Você não definiu um formato de saída em nenhum domínio no tutorial.  
  
     ![Página resultados da limpeza de exportação](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "página resultados da limpeza de exportação")  
  
4.  Clique em **exportar** para exportar os dados. Não clique **concluir** ainda.  
  
5.  Clique em **feche** sobre o **exportando** caixa de diálogo.  
  
6.  Clique em **concluir** para concluir a atividade. Se você se esqueceu de exportar os resultados antes de clicar em **terminar**, clique em **Abrir projeto de qualidade de dados** na página principal do **cliente DQS**, selecione **Supplier limpar Lista** na lista de projetos e clique em **próxima** na parte inferior da tela para obter o **exportar** estágio do processo de limpeza novamente. Você também pode mudar para **gerenciar e exibir resultados** guia clicando **volta** botão.  
  
7.  Abra o **Cleansed Supplier List** e faça o seguinte:  
  
    1.  Certifique-se de que não há nenhum endereço de email que termine com Adventure-Work.com (sem o caractere ') procurando Adventure-Work.com na planilha.  
  
    2.  Veja que não há nenhuma **EUA** valor na **país** coluna.  
  
    3.  Pesquise **Los Angeles** e ver que o **estado** está definido como **CA**.  
  
    4.  Confirme se não houver nenhum termos **co**, **corp.**, e **Inc.**.  
  
    5.  Excluir o **Address Validation** coluna da planilha e salve o arquivo do excel. Essa coluna adicional corresponde ao domínio composto Address Validation.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Importando valores do fornecedor projeto Limpar lista](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
