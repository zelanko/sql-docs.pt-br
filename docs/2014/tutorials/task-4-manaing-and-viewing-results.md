---
title: 'Tarefa 4: Gerenciando e exibindo resultados | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2df7517a8043269efe40d21b112100edaf9e847f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489452"
---
# <a name="task-4-manaing-and-viewing-results"></a>Tarefa 4: Gerenciando e exibindo resultados
  Nesta tarefa, você revisará os resultados da limpeza auxiliada por computador, além de executar a limpeza interativa nos dados do fornecedor. Ver [estágio de limpeza interativa](https://msdn.microsoft.com/library/hh213061.aspx#Interactive) para obter mais detalhes.  
  
1.  Selecione **Contact Email** domínio na lista de domínios.  
  
2.  Alterne para o **inválido** guia no painel à direita. Observe que dois endereços de email não tinham o caractere ' no final. Esses dois email foram considerado inválidos pela regra de domínio que exige que todos os endereços de email terminem com **@adventure-works.com** (do '). O DQS usa a regra de domínio enquanto faz a limpeza para determinar se um email é válido ou não. Essa guia exibe os valores de domínio que foram marcados como inválidos na base de dados de conhecimento ou que não estavam de acordo com uma regra de domínio. Nesse caso, esses valores não estavam em conformidade com a regra de domínio (Email Validation).  
  
3.  No **corrigir para** coluna, digite o certo endereço de email que terminam com **@adventure-works.com** (do ').  
  
     ![Correções de regra de validação de Email](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "correções de regra de validação de Email")  
  
4.  Clique em **aprovar** para ambos os registros aprovem ambas as alterações. Quando você aprovar, os registros serão movidos para o **corrigido** guia. Em vez de aprovar cada item separadamente, você pode aprovar todas as alterações ao mesmo tempo usando o **aprovar todos os termos** botão da barra de ferramentas.  
  
5.  Alterne para o **New** guia no painel à direita. Os valores dessa guia são os valores para os quais o DQS ainda não tem informações suficientes na base de dados de conhecimento para determinar se eles estão corretos. Consequentemente, ele não pode modificar nem sugerir alterações para os valores de domínio.  
  
6.  Examine os valores para confirmar que todos os emails terminam com **@adventure-works.com** e clique em **aprovar todos os termos** na barra de ferramentas. Os valores aprovados nessa guia movem para o **corrija** guia.  
  
7.  Selecione o **país** domínio na lista de domínios.  
  
8.  Alterne para o **corrigido** guia no painel direito e observe que **United State** valor será corrigido automaticamente para o **dos Estados Unidos** do ' no final. Essa regra não é uma regra definida para o **país** é de domínio, mas o DQS **83%** certeza de que o valor correto é **dos Estados Unidos**. O **aprovar** botão é selecionado automaticamente para todos os **corrigido** itens. Você pode substituir esse comportamento e rejeitar uma alteração.  
  
9. Observe que **EUA** foi corrigido para **dos Estados Unidos** porque eles são sinônimos e **dos Estados Unidos** é o valor principal (preferencial).  
  
     ![Correções com base em sinônimos](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "correções com base em sinônimos")  
  
10. Observe que o **aprovar** botão já está selecionado para esses valores corrigidos. Esse é o comportamento padrão para os valores corrigidos. Você pode rejeitar uma alteração e quando você fizer isso, o valor passa para o **inválido** guia.  
  
11. Selecione **Supplier Name** da lista de domínios.  
  
12. Alterne para o **corrigido** guia no painel à direita.  
  
     ![Nomes de fornecedores corrigidos](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "nomes de fornecedores corrigidos")  
  
    1.  Observe que **r. Datum corp.** foi corrigido para **A. Datum Corporation** e o **motivo** é definido como **relação baseada em termos. A. datum Corporation** é um valor de domínio conhecido DQS, pois ele foi descoberto durante o processo de descoberta de Conhecimento. Portanto, o DQS está **100% seguro** dessa correção.  
  
    2.  Observe que **Lazy Country Storex** foi corrigido para **Lazy Country Store**, **nível de confiança** é definido como **100%** e o **Motivo** é definido como **valor de domínio**. Durante o processo de descoberta de Conhecimento, você deve definir **Lazy Country Storex** como um erro com **Lazy Country Store** como o **correção**, portanto, o DQS é **100% confiante** dessa correção.  
  
    3.  O DQS não está familiarizado com os outros valores na lista, mas encontrou as correções para esses valores usando o **verificador ortográfico** e propõe as correções apropriadas. O DQS está **não 100%** está confiante sobre essas correções, mas o nível de confiança acima de 80%, que é o nível de limite para fazer correções; portanto, o DQS propõe as correções.  
  
13. Observe que o **aprovar** é habilitado automaticamente para todos os valores. Você pode substituir o valor corrigido ou rejeitar as alterações conforme apropriado. Por padrão o **aprovar** botão é selecionado para todos os valores na **corrigido** guia.  
  
14. Alterne para o **New** guia.  
  
15. Observe que **corp.** foi corrigido para **Corporation**, **co** foi corrigido para **empresa**, e **Inc.** foi corrigido para **Incorporated**. Por exemplo, **Consolidate Inc.** foi corrigido para **Consolidate Incorporated** e **Consolidated co.** foi corrigido para **Consolidated Company**, e **Frabrikam corp.** foi corrigido para **Fabrikam Corporation**.  Você pode ver que **relação baseada em termos** é mencionada como motivo. Essas alterações são proposta por meio das relações baseadas em termos que você definiu durante a atividade de gerenciamento de domínio. Você pode alterar o **corrigir para** os valores manualmente aqui.  
  
16. Role a lista para ver **Hunxgry Coyote Store** com uma linha ondulada vermelha. Clique com botão direito nela e clique em **Hungy Coyote Store** (com sem ' x'). O **corrigir para** coluna deve ser preenchida automaticamente com **Hungry Coyote Store**. Você também pode digitar manualmente um valor na coluna Corrigir para.  
  
17. Clique em **aprovar todos os termos** na barra de ferramentas. Os valores de domínio com o **corrigir para** mover do valor especificado para o **corrigido** guia e os novos valores sem nenhum associados **correto para** valores movem para o  **Correto** guia.  
  
18. Selecione o **Address Validation** domínio composto na lista de domínios.  
  
19. No painel direito, alterne para o **corrija** guia. Você deve ver os endereços que são considerados corretos pelo **Melissa Data – Address Check** serviço DQS na **do Azure Marketplace**.  
  
20. Alterne para o **corrigido** guia.  
  
21. Observe que **estado** para o registro que tem **City** como **Los Angeles** é definido como **CA** agora. Observe a **motivo** campo é que **corrigido pela regra 'City-State Rule'**.  
  
     ![Correção de regra City-State](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "City-State correção de regra")  
  
22. Observe que o **aprovar** botão de opção já está selecionado para este item na lista. Isso é o comportamento padrão para itens na **corrigido** guia.  
  
23. Alterne para o **sugerido** guia. Revise as alterações sugeridas pelo **Melissa Data – Address Check** service.  
  
24. **Clique em Aprovar todos os termos** no botão de barra de ferramentas e clique **Okey** sobre o **confirmação** caixa de mensagem.  
  
     ![Aprovar todos os botões de barra de ferramentas de termos](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "aprovar todos os botões de barra de ferramentas de termos")  
  
25. Clique em **próxima** para alternar para o **exportar** página.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Exportando os resultados para um arquivo do Excel da limpeza](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
