---
title: Criar uma regra de domínio cruzado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.testcdrule.f1
- sql12.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 9478564d6fde6596fe6f407bb9a9a2b389b2a1d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480995"
---
# <a name="create-a-cross-domain-rule"></a>Criar uma regra de domínio cruzado
  Este tópico descreve como criar uma regra de domínio cruzado para um domínio composto em uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Uma regra de domínio cruzado testa a relação entre valores de domínios únicos que são incluídos em um domínio composto. A regra de domínio cruzado deve se repetir em um domínio composto para que os valores do domínio sejam considerados precisos e em conformidade com os requisitos comerciais. Uma regra de domínio cruzado é usada para validar, corrigir e unificar valores de domínio.  
  
 As cláusulas If e Then de uma regra de domínio cruzado são definidas para um dos domínios únicos do domínio composto. Cada cláusula deve ser definida para um único domínio diferente. Uma regra de domínio cruzado deve se relacionar a vários domínios únicos; você não pode definir uma regra de domínio simples (destinada a um domínio único) para um domínio composto. Você faria isso definindo uma regra de domínio para um domínio único. As cláusulas If e Then podem contar uma ou mais condições cada uma.  
  
 Uma regra de domínio cruzado que tem condições definitivas aplicará a lógica de regras a sinônimos do valor nas condições, bem como os próprios valores. As condições definitivas das cláusulas If e Then são Valor é igual a, Valor não é igual a, Valor está em ou Valor não está em. Por exemplo, suponhamos que você tenha a seguinte regra de domínio cruzado para um domínio composto: "Para ‘Cidade’, se Valor é igual a ‘Los Angeles’, então para ‘Estado’, Valor é igual a ‘CA’. "Se 'Los Angeles' e 'LA' forem sinônimos, esta regra retornará correto para 'Los Angeles CA' e 'LA CA' e com erro para 'Los Angeles WA' e 'LA WA'.  
  
 Além de informar você sobre a validade de uma regra de domínio cruzado, a cláusula *Then* definitiva em uma regra de domínio cruzado, **Valor é igual a**, também corrige os dados durante a atividade de limpeza de dados. Para obter mais informações, consulte [Data Correction using Definitive Cross-Domain Rules](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) em [Cleanse Data in a Composite Domain](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md).  
  
 As regras de domínio cruzado são levadas em consideração depois de todas as regras simples que afetam apenas um domínio único. Apenas se um valor estiver de acordo com as regras de domínio único (caso elas existam), a regra de domínio cruzado será aplicada. O domínio composto e os domínios únicos nos quais uma regra é executada devem ser definidos para que a regra possa ser executada.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para criar uma regra de domínio cruzado, você deve criar e abrir um domínio composto.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma regra de domínio cruzado.  
  
##  <a name="Create"></a>Criar regras entre domínios  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra ou crie uma base de dados de conhecimento. Selecione **Gerenciamento de Domínio** como a atividade e, depois, clique em **Abrir** ou **Criar**. Para obter mais informações, consulte [Criar uma base de dados de conhecimento](../../2014/data-quality-services/create-a-knowledge-base.md) ou [Abrir uma base de dados de conhecimento](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  O gerenciamento de domínio é executado em uma página do cliente Data Quality Services que contém cinco guias para operações de gerenciamento de domínio separadas. Não se trata de um processo controlado por assistente; qualquer operação de gerenciamento pode ser executada separadamente.  
  
3.  Na **Lista de domínios** na página **Gerenciamento de Domínio** , selecione o domínio composto para o qual você deseja criar uma regra de domínio ou crie um novo domínio composto. Se você precisar criar um novo domínio, consulte [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md).  
  
4.  Clique na guia **Regras do CD** .  
  
5.  Clique em **Adicione uma nova regra de domínio**e forneça um nome e uma descrição para a regra.  
  
6.  Selecione **Ativa** para especificar que a regra será executada (o padrão) e anule a seleção para impedir a execução da regra.  
  
7.  Crie a cláusula If da seguinte maneira:  
  
    1.  Na lista de domínios do painel da cláusula If, selecione um dos domínios únicos incluídos no domínio composto para ser o assunto da cláusula If. Você pode selecionar qualquer domínio único no domínio composto.  
  
    2.  Selecione uma condição na lista suspensa como a primeira condição da cláusula.  
  
    3.  Se a condição exigir um valor, insira o valor na caixa de texto associada à condição.  
  
    4.  Se a cláusula If exigir outra condição, clique em **Adiciona uma nova condição à cláusula selecionada**. Selecione o operador, selecione uma condição e insira um valor para a condição, se necessário.  
  
    5.  Para alterar a ordem das condições, selecione uma condição clicando à sua esquerda e clique na seta para cima ou seta para baixo.  
  
    6.  Para ocultar as condições, clique no sinal de subtração à esquerda do nome do domínio. Clique no sinal de adição para exibir as condições.  
  
8.  Crie a cláusula Then selecionando um domínio único, que não seja o assunto da cláusula If, na lista de domínios do painel da cláusula Then. Em seguida, compile a cláusula Then usando as mesmas etapas executadas na compilação da cláusula If.  
  
9. Continue o procedimento de teste a seguir.  
  
##  <a name="Test"></a>Testar regras de domínio cruzado  
  
1.  Teste a regra de domínio cruzado da seguinte maneira:  
  
    1.  Clique no ícone **Executar a regra de domínio selecionada em dados de teste** no canto superior direito do painel de domínio composto.  
  
    2.  Na caixa de diálogo **Testar Regra de Domínio** , clique no ícone **Adiciona um Novo Termo de Teste para a Regra de Domínio** .  
  
    3.  Insira valores de teste para o domínio único associado à cláusula If e o domínio único associado à cláusula Then. Os valores de teste inseridos na cláusula If devem atender às condições dessa cláusula, ou um ponto de interrogação será inserido na coluna **Validade** indicando que a regra de domínio cruzado não se aplicará aos dados de teste.  
  
    4.  Clique no ícone **Adiciona um novo termo de teste para a regra de domínio** novamente para adicionar outro conjunto de valores de teste.  
  
    5.  Clique no ícone **Teste a Regra de Domínio em Todos os Termos** . Se um conjunto de valores de teste for válido, o DQS inserirá uma marca de verificação na coluna **Validade** para a linha. Se o conjunto de valores de teste não for válido, o DQS inserirá um triângulo com um ponto de exclamação na coluna Validade da linha.  
  
    6.  Depois que os testes forem concluídos, clique em **Fechar** na caixa de diálogo **Testar Regra de Domínio Composto** .  
  
2.  Quando você concluído as regras de domínio cruzado, clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [End the Domain Management Activity](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="FollowUp"></a>Acompanhamento: depois de criar uma regra de domínio cruzado  
 Após criar uma regra de domínio cruzado, você poderá executar outras tarefas de gerenciamento de domínio no domínio, poderá executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou poderá adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
