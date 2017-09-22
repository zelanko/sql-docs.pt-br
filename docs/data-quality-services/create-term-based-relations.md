---
title: "Criar relações baseadas em termos | Microsoft Docs"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 93965e0267bb988b2b833701c9f193385220ff90
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="create-term-based-relations"></a>Criar relações baseadas em termos
  Este tópico descreve como criar relações baseadas em termos para um domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Uma relação baseada em termos permite que você faça uma correção em um termo que faz parte de um valor em um domínio. Elas permitem que diversos valores idênticos, exceto pela ortografia de uma parte comum deles, sejam considerados como sinônimos idênticos. Por exemplo, você pode configurar uma relação baseada em termos que altere o termo “Inc.” para “Incorporated”. O termo “Inc.” será alterado toda vez que ocorrer no domínio. Instâncias de "Contoso, Inc." serão alteradas para "Contoso, Incorporated", e os dois valores serão considerados sinônimos exatos.  
  
 Para usar relações baseadas em termos, crie uma lista de pares Valor/Corrigir para, como "Inc." e "Incorporated" ou "Senior" e "Sr.". O uso de uma relação baseada em termos lhe permite alterar um termo ao longo do domínio, sem definir valores de domínio individuais manualmente como sinônimos. Você pode especificar que um valor seja corrigido, mesmo que a descoberta da base de dados de conhecimento não tenha descoberto esse valor antes. Se uma transformação de relação baseada em termos levar dois valores a serem idênticos, o DQS criará uma relação de sinônimo entre eles (em descoberta da base de dados de conhecimento), uma relação de correção entre eles (em correção de dados), ou uma correspondência exata (em correspondência).  
  
 A transformação de relações baseadas em termos e a transformação de símbolos (na qual caracteres especiais são substituídos por um espaço ou um nulo) são ambas realizadas em uma fase de pré-processamento antes da análise. Se a análise de domínio composto for solicitada, ela será executado antes das duas transformações, pois a análise de delimitador requer símbolos. Outras operações, como regras de domínio e alterações de valor de domínio, serão executadas depois das transformações. Para a correspondência, as relações com base em termos são aplicadas nos dados de origem antes da atividade de correspondência mesmo que você não execute a limpeza.  
  
 **Relações baseadas em termos e gerenciamento de domínio**  
  
 Quando você aplicar uma relação baseada em termos no gerenciamento de domínio, o DQS aplicará as alterações na descoberta de conhecimento, processos de limpeza ou correspondência; porém, o DQS não altera o próprio valor de domínio para ser compatível com a relação baseada em termos. Em outras palavras, se você inserir e aceitar uma relação baseada em termos, na guia **Relações Baseadas em Termos** da página **Gerenciamento de Domínio** , a alteração não será feita na guia **Valores de Domínio** da mesma página. Isto permite que você altere o TBR subsequentemente.  
  
 **Relações baseadas em termos e limpeza de dados**  
  
 Quando você aplicar uma relação baseada em termos em um domínio e executar o processo de limpeza de dados, o DQS aplicará as alterações durante a limpeza, mas não aplicará as alterações aos termos na base de dados de conhecimento.  
  
-   Se um valor, conforme tiver sido alterado por uma relação baseada em termos, estiver no domínio, mas não for um sinônimo, ele será mostrado na coluna **Corrigir para** na guia **Corrigido** da página **Gerenciar e Exibir resultados** , com a Razão definida como Relação baseada em termos.  
  
-   Se um valor, conforme tiver sido alterado por uma relação baseada em termos, não estiver no domínio e o DQS localizar um valor compatível, o valor será corrigido para isto e aparecerá sob a guia Corrigido ou a guia Sugerido, com base no nível de confiança. Se nenhuma correspondência for localizada, o valor aparecerá abaixo de Novo com uma correção de TBR. Isto será feito porque, mesmo que você corrija o TBR, isso não significará que o valor esteja correto.  
  
-   Se um valor, conforme tiver sido alterado por uma relação baseada em termos, estiver no domínio, mas o valor for Erro/Inválido com a correção existente, o valor aparecerá sob a guia Corrigido com sua correção e a razão Valor de Domínio.  
  
-   Se um valor, conforme tiver sido alterado por uma relação baseada em termos, estiver no domínio, mas o valor for Erro/Inválido sem correção, o valor aparecerá sob a guia Inválido com a razão Valor de Domínio.  
  
 **Relações baseadas em termos e descoberta da base de dados de conhecimento**  
  
 Quando você aplicar uma relação baseada em termos e em seguida executar o processo de descoberta da base de dados de conhecimento, qualquer valor compatível com o TBR permanecerá igual e será identificado como um valor correto. Qualquer valor que for alterado por um TBR será importado como um valor correto e será identificado como um sinônimo para um valor compatível com o TBR.  
  
 **Relações baseadas em termos e importar valores de limpeza para um domínio**  
  
 Se você importar uma base de conhecimento de qualidade de dados coletada durante o processo de limpeza para um domínio, um valor que é alterado por um TBR será importado como um valor correto.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para criar relações baseadas em termos, você deve ter um domínio aberto na atividade Gerenciamento de Domínio.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar relações baseadas em termos.  
  
##  <a name="Create"></a> Criar relações baseadas em termos  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra ou crie uma base de dados de conhecimento. Selecione **Gerenciamento de Domínio** como a atividade e, depois, clique em **Abrir** ou **Criar**. Para obter mais informações, consulte [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) ou [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  O gerenciamento de domínio é executado em uma página do cliente Data Quality Services que contém cinco guias para operações de gerenciamento de domínio separadas. Não se trata de um processo controlado por assistente; qualquer operação de gerenciamento pode ser executada separadamente.  
  
3.  Na **Lista de domínios** na página **Gerenciamento de Domínio** , selecione o domínio para o qual você deseja criar uma regra de domínio ou crie um novo domínio. Se você precisar criar um novo domínio, consulte [Create a Domain](../data-quality-services/create-a-domain.md).  
  
4.  Clique na guia **Relações Baseadas em Termos** .  
  
5.  Crie relações baseadas em termos desta forma:  
  
    1.  Clique em **Adicionar Nova Relação** para adicionar uma linha à tabela Relações.  
  
    2.  Para a coluna **Valor** da linha adicionada, insira um termo que você deseja alterar toda vez que ele ocorrer em um valor no domínio selecionado.  
  
        > [!NOTE]  
        >  Você obterá um erro se o termo existir como um valor inteiro no domínio, ou se ele já existir como um valor corrigido no domínio.  
  
    3.  Na coluna **Corrigir para** , insira um termo desejado para alterar o termo na coluna **Valor** .  
  
    4.  Clique novamente em **Adicionar Novas Relações** para adicionar outra relação baseada em termos.  
  
    5.  Clique em **Excluir Relações Selecionadas** para excluir uma ou mais linhas selecionadas da tabela Relações. Você pode selecionar várias linhas pressionando o botão Ctrl e clicando em uma linha não selecionada.  
  
    6.  Localize um valor na tabela Relações inserindo um ou mais dígitos na caixa de texto **Localizar** . Correspondências para a cadeia de caracteres serão realçadas. Use as setas para cima e para baixo para se mover para instâncias diferentes da cadeia de caracteres na tabela.  
  
    7.  **Verificador Ortográfico**: se um valor na coluna **Valor** ou **Corrigir para** tiver um sublinhado vermelho ondulado, o Verificador Ortográfico sugerirá uma correção para o valor. Clique com o botão direito do mouse no valor com sublinhado e selecione um dos valores propostos pelo Verificador Ortográfico. Como alternativa, você pode clicar em **Adicionar** no menu de atalho para continuar com o valor original. Para obter mais informações, consulte [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md) e [Set Domain Properties](../data-quality-services/set-domain-properties.md).  
  
        > [!NOTE]  
        >  Para usar o Verificador Ortográfico, você pode habilitá-lo na página **Propriedades de Domínio** ou, se ele estiver desabilitado na página **Propriedades de Domínio** , você poderá clicar no ícone **Habilitar/Desabilitar o Verificador Ortográfico** na página **Relações Baseadas em Termos** para habilitá-lo nessa página.  
  
6.  Clique em **Aplicar Alterações** para aplicar as relações baseadas em termos no domínio.  
  
7.  Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="FollowUp"></a> Acompanhamento: após criar relações baseadas em termos  
 Depois de criar relações baseadas em termos, você poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md).  
  
  
