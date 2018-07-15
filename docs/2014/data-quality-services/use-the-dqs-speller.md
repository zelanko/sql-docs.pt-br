---
title: Usar o verificador ortográfico do DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65e4e53e-2699-4cae-a9e0-fe78547755b5
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 237b63e0eda22e1676a7e12ffcc2166c40d2b0ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202006"
---
# <a name="use-the-dqs-speller"></a>Usar o verificador ortográfico DQS
  O verificador ortográfico do [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) verifica a sintaxe, a ortografia e a estrutura de frase de valores da cadeia de caracteres em um domínio. O verificador ortográfico é um recurso autônomo, do lado do cliente, sem integração com mecanismos do lado do servidor e sem implicações em fluxos ou status atuais. O verificador ortográfico identifica esses valores da cadeia de caracteres que considera serem erros potenciais e, então, marca-os com um sublinhado vermelho no mesmo local no qual você faz outras alterações manuais em valores de domínio. Esses locais incluem:  
  
-   A página **Gerenciar Valores de Domínio** da atividade **Descoberta da Base de Dados de Conhecimento**  
  
-   A página **Valores de Domínio** ou a página **Relações Baseadas em Termos** da atividade **Gerenciamento de Domínio**  
  
-   A página **Gerenciar e Exibir resultados** da atividade de **Limpeza**  
  
 O verificador ortográfico só funciona em domínios únicos com um tipo de dados string. Todos os valores em um único domínio que são de um tipo de dados string são enviados ao verificador ortográfico para validação. O verificador ortográfico não funciona para um domínio composto e não funciona para domínios de tipos que não sejam string, valores mistos (como letras e números sem espaço), numerais romanos, caracteres únicos e valores que consistem apenas em letras maiúsculas.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para executar o verificador ortográfico, você deve ter uma base de dados de conhecimento e um domínio aberto na atividade Descoberta de Conhecimento ou Gerenciamento de Domínio; o verificador ortográfico deve estar habilitado para o domínio e na página onde você vai executá-lo; e a propriedade de idioma deve ser especificada para o domínio.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 É necessário ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para executar o verificador ortográfico.  
  
##  <a name="Enable"></a> Habilitar o verificador ortográfico  
  
1.  Para habilitar o verificador ortográfico no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], abra a base de dados de conhecimento na atividade **Gerenciamento de Domínio** , selecione o domínio desejado e clique em **Habilitar Verificador Ortográfico** na página **Propriedades de Domínio** . Em **Idioma**, selecione o idioma a ser usado com o verificador ortográfico.  
  
2.  Quando o verificador ortográfico está habilitado nas propriedades de domínio, ele está habilitado na página **Gerenciar de Valores de Domínio** , na página **Valores de Domínio** ou na página **Relações Baseadas em Termos** , e na página **Gerenciar e Exibir resultados** . Para desabilitar o verificador ortográfico nestes páginas, clique no ícone **Habilitar/Desabilitar o Verificador Ortográfico** . Quando você clica no ícone, altera o status do verificador ortográfico na página. Da mesma forma, se a propriedade **Habilitar Verificador Ortográfico** para o domínio estiver desabilitada, ao clicar no ícone **Habilitar/Desabilitar o Verificador Ortográfico** , você habilitará o verificador ortográfico na página. Se você sair da página e retornar a ela, o status de botão será determinado novamente pela propriedade de domínio **Habilitar Verificador Ortográfico** .  
  
##  <a name="Use"></a> Usar o verificador ortográfico  
  
1.  Mova para uma das seguintes páginas:  
  
    -   A página **Gerenciar Valores de Domínio** da atividade **Descoberta da Base de Dados de Conhecimento**  
  
    -   A página **Valores de Domínio** ou a página **Relações Baseadas em Termos** da atividade **Gerenciamento de Domínio**  
  
    -   A página **Gerenciar e Exibir resultados** da atividade de **Limpeza**  
  
2.  Exiba os valores apropriados na tabela **Valor** , filtrando ou pesquisando.  
  
3.  Examine as linhas na tabela **Valor** para determinar se qualquer valor na coluna **Valor** ou **Corrigir para** está marcado com um sublinhado vermelho ondulado.  
  
4.  Clique com o botão direito do mouse em um valor marcado por um sublinhado vermelho. Clique em um dos valores de substituição listados se ele for preferível ao valor original.  
  
5.  Se nenhum valor exibido for preferível, e houver um botão **Mais sugestões** indicando valores adicionais, clique nele. Se um dos valores adicionais for preferível ao valor original, clique nele.  
  
6.  Se você desejar adicionar o valor ao dicionário, clique em **Adicionar ao Dicionário**. O sublinhado vermelho desaparecerá do valor.  
  
##  <a name="FollowUp"></a> Acompanhamento: após usar o verificador ortográfico  
 Após executar o verificador ortográfico, conclua a atividade do domínio para usar as correções sugeridas pelo verificador ortográfico. Se estiver na atividade de descoberta da base de dados de conhecimento, gerenciamento de domínio ou política de correspondência, publique a base de dados de conhecimento para disponibilizar os resultados da análise do verificador ortográfico para uso na base de dados de conhecimento. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="How"></a> Como o verificador ortográfico funciona  
 O verificador ortográfico do DQS marca qualquer erro em potencial de valor da cadeia de caracteres com um sublinhado vermelho que é exibido para o valor inteiro. Por exemplo, se “New York” estivesse escrito incorretamente como “Neu York”, o verificador ortográfico exibiria um sublinhado vermelho em “Neu York”, e não apenas em “Neu”. Se você clicar com o botão direito do mouse no valor, verá as correções sugeridas para o valor inteiro. Você também pode clicar em **Mais sugestões** quando há mais de cinco sugestões. Você pode escolher uma das sugestões ou adicionar um valor ao dicionário (em nível de conta de usuário) a ser exibido para o valor original. Valores adicionados ao dicionário se aplicam a todos os domínios. Somente se você designar explicitamente uma sugestão, a correção será feita no domínio. Quando você seleciona uma sugestão no menu de contexto do verificador ortográfico, o tipo de valor se torna (ou permanece como) um erro. A sugestão selecionada será adicionada à coluna de correção. Observe que o **Tipo** de um valor pode ser **Correto** e ele ainda ser marcado como um erro potencial pelo verificador ortográfico.  
  
 O DQS fornecerá sugestões para valores nas colunas **Valor** e **Corrigir para** da tabela **Valor** . Quando você seleciona uma sugestão na coluna **Valor** , o tipo de valor é definido como **Erro**e a sugestão é copiada para a coluna **Corrigir para** , como se ela tivesse sido inserida manualmente. Caso exista uma correção, ela se tornará uma sugestão. Na página **Gerenciar e Exibir resultados** da atividade de **Limpeza** , quando você seleciona uma sugestão na coluna **Corrigir para** , o DQS substitui o valor selecionado no momento pela seleção, e o valor selecionado no momento se torna uma sugestão. Na página **Gerenciar e Exibir resultados** da atividade de **Limpeza** , não há sugestões no nível de registro (a grade inferior).  
  
  
