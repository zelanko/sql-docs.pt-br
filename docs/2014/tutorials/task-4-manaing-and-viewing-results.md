---
title: 'Tarefa 4: Manaing e exibindo resultados | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ef2599ea202fad2b85881951692f1f04898e94e8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006568"
---
# <a name="task-4-manaing-and-viewing-results"></a>Tarefa 4: Gerenciando e exibindo resultados
  Nesta tarefa, você revisará os resultados da limpeza auxiliada por computador, além de executar a limpeza interativa nos dados do fornecedor. Consulte [estágio de limpeza interativa](https://msdn.microsoft.com/library/hh213061.aspx#Interactive) para obter mais detalhes.  
  
1.  Selecione **contato** de domínio de email na lista de domínios.  
  
2.  Alterne para a guia **inválido** no painel direito. Observe que dois endereços de email que estavam com caracteres ' s ausentes no final. Esses dois emails que foram considerados inválidos pela regra de domínio que exigem que todos os endereços de email terminem com ** \@ Adventure-Works.com** (com '). O DQS usa a regra de domínio enquanto faz a limpeza para determinar se um email é válido ou não. Essa guia exibe os valores de domínio que foram marcados como inválidos na base de dados de conhecimento ou que não estavam de acordo com uma regra de domínio. Nesse caso, esses valores não estavam em conformidade com a regra de domínio (Email Validation).  
  
3.  Na coluna **corrigir para** , digite o endereço de email correto que termina com ** \@ Adventure-Works.com** (com ').  
  
     ![Regra de validação Correções de Email](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "Regra de validação Correções de Email")  
  
4.  Clique em **aprovar** para os dois registros para aprovar as duas alterações. Quando você aprova, os registros são movidos para a guia **corrigido** . Em vez de aprovar cada item separadamente, você pode aprovar todas as alterações ao mesmo tempo usando o botão de barra de ferramentas **aprovar todos os termos** .  
  
5.  Alterne para a **nova** guia no painel direito. Os valores dessa guia são os valores para os quais o DQS ainda não tem informações suficientes na base de dados de conhecimento para determinar se eles estão corretos. Consequentemente, ele não pode modificar nem sugerir alterações para os valores de domínio.  
  
6.  Examine os valores para confirmar se todos os emails terminam com ** \@ Adventure-Works.com** e clique em **aprovar todos os termos** na barra de ferramentas. Os valores aprovados dessa guia se movem para a guia **correta** .  
  
7.  Selecione o domínio **país** na lista de domínios.  
  
8.  Alterne para a guia **corrigido** no painel direito e observe que o valor do **estado United** é corrigido automaticamente para a **Estados Unidos** com ' s' no final. Essa regra não é uma regra que você definiu para o domínio do **país** , mas o DQS é **83%** de confiança de que o valor correto é **Estados Unidos**. O botão **aprovar** é selecionado automaticamente para todos os itens **corrigidos** . Você pode substituir esse comportamento e rejeitar uma alteração.  
  
9. Observe que os **EUA** foram corrigidos para **Estados Unidos** porque são sinônimos e **Estados Unidos** é o valor principal (preferencial).  
  
     ![Correções com base em sinônimos](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "Correções com base em sinônimos")  
  
10. Observe que o botão **aprovar** já está selecionado para esses valores corrigidos. Esse é o comportamento padrão para os valores corrigidos. Você pode rejeitar uma alteração e, ao fazer isso, o valor é movido para a guia **inválida** .  
  
11. Selecione **nome do fornecedor** na lista de domínios.  
  
12. Alterne para a guia **corrigido** no painel direito.  
  
     ![Nomes de fornecedores corrigidos](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "Nomes de fornecedores corrigidos")  
  
    1.  Observe que **a. Datum Corp.** é corrigida para a **a. Datum Corporation** e o **motivo** é definido como **relação baseada em termos. A. Datum Corporation** é um valor de domínio conhecido para o DQS, pois ele foi descoberto durante o processo de descoberta do conhecimento. Portanto, o DQS tem **100% de confiança** sobre essa correção.  
  
    2.  Observe que **o Storex de país lento** é corrigido para o **repositório de país lento**, o **nível de confiança** é definido como **100%** e o **motivo** é definido como **valor de domínio**. Durante o processo de descoberta da base de dados de conhecimento, você define o **Storex do país lento** como um erro com o **repositório de país lento** como a **correção**; portanto, o DQS é de **100% confiante** em fazer essa correção.  
  
    3.  O DQS não está familiarizado com os outros valores da lista, mas encontrou as correções para esses valores usando o **Verificador ortográfico** e propõe as correções apropriadas. O DQS não tem mais de **100%** de confiança sobre essas correções, mas o nível de confiança está acima de 80%, que é o nível de limite para fazer correções, de modo que o DQS propõe as correções.  
  
13. Observe que a **aprovação** é habilitada automaticamente para todos os valores. Você pode substituir o valor corrigido ou rejeitar as alterações conforme apropriado. Por padrão, o botão **aprovar** é selecionado para todos os valores na guia **corrigido** .  
  
14. Alterne para a **nova** guia.  
  
15. Observe que **Corp.** é corrigido para a **corporação**, **co.** é corrigido para a **empresa**, e **Inc.** é corrigido para **incorporado**. Por exemplo, **consolidar Inc.** é corrigido para consolidar o co **incorporado** e **consolidado.** o é corrigido para a **empresa consolidada**e a **Frabrikam Corp.** é corrigida para a **Fabrikam Corporation**.  Você pode ver que a **relação baseada em termos** é mencionada como o motivo. Essas alterações são proposta por meio das relações baseadas em termos que você definiu durante a atividade de gerenciamento de domínio. Você pode alterar os valores **corretos** manualmente aqui.  
  
16. Role a lista para ver a **Hunxgry coiote Store** com uma linha ondulada vermelha. Clique com o botão direito do mouse nele e clique em **coiote de armazenamento suspenso** (sem ' x '). A coluna **corrigir para** deve ser preenchida automaticamente com o **coiote Store de fome**. Você também pode digitar manualmente um valor na coluna Corrigir para.  
  
17. Clique em **aprovar todos os termos** na barra de ferramentas. Os valores de domínio com o valor **correto para** especificado são movidos para a guia **corrigido** e os novos valores sem valores **corretos de corrigir para** se movem para a guia **correta** .  
  
18. Selecione a **validação de endereço** domínio composto na lista domínio.  
  
19. No painel direito, alterne para a guia **correto** . Você deve ver os endereços que estão corretos no serviço do DQS da **verificação de endereço de dados do Melissa** no **Azure Marketplace**.  
  
20. Alterne para a guia **corrigido** .  
  
21. Observe que o **estado** do registro que tem a **cidade** como **los Angeles** está definido como **CA** agora. Observe que, no campo **motivo** **, é corrigido pela regra "cidade-estado**da regra".  
  
     ![Correção de Regra Cidade-Estado](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "Correção de Regra Cidade-Estado")  
  
22. Observe que o botão de opção **aprovar** já está selecionado para este item na lista. Esse é o comportamento padrão para itens na guia **corrigido** .  
  
23. Alterne para a guia **sugerida** . revise as alterações sugeridas pelo serviço de **verificação de endereço de dados Melissa** .  
  
24. **Clique em aprovar todos os termos** no botão da barra de ferramentas e clique em **OK** na caixa de mensagem de **confirmação** .  
  
     ![Botão de barra de ferramentas Aprovar Todos os Termos](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "Botão de barra de ferramentas Aprovar Todos os Termos")  
  
25. Clique em **Avançar** para alternar para a página **Exportar** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Exportando os resultados da limpeza para um arquivo do Excel](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
