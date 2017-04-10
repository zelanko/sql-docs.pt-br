---
title: "Criar um dom&#237;nio | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.kb.createdomain.f1"
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# Criar um dom&#237;nio
  Este tópico descreve como criar um domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Os valores no domínio são uma representação semântica dos dados em um campo. Para obter mais informações sobre domínios, consulte [Gerenciando um domínio](../data-quality-services/managing-a-domain.md).  
  
 Há duas maneiras de criar um novo domínio. A primeira é durante a etapa Mapear da atividade de descoberta da base de dados de conhecimento, quando você está no processo de analisar um exemplo de dados para adicionar conhecimento a uma base de dados de conhecimento nova ou existente. A segunda é durante a atividade de gerenciamento de domínio, quando, em vez de alterar um domínio existente, você cria um novo domínio.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para criar um domínio, você precisa ter criado e aberto uma base de dados de conhecimento.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou o dqs_administrator no banco de dados DQS_MAIN para criar um domínio.  
  
##  <a name="Discovery"></a> Criar um domínio na atividade Descoberta da Base de Dados de Conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento** e selecione uma base de dados de conhecimento ou clique em **Nova base de dados de conhecimento** e insira propriedades para a nova base de dados de conhecimento.  
  
3.  Selecione **Descoberta da Base de Dados de Conhecimento** como a atividade e clique em **Criar** para criar a nova base de dados de conhecimento ou em **Abrir** para abrir uma base de dados de conhecimento existente.  
  
4.  Na página **Mapa** , especifique uma conexão com a fonte de dados. Para obter mais informações, consulte [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
5.  No **mapeamentos** da tabela, selecione uma coluna de origem na lista suspensa para o **coluna de origem** coluna de uma linha vazia. Se não existir nenhum domínio correspondente, clique o **criar um domínio** ícone.  
  
##  <a name="DomainManagement"></a> Criar um domínio na atividade Gerenciamento de Domínio  
  
1.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento** e selecione uma base de dados de conhecimento ou clique em **Nova base de dados de conhecimento** e insira propriedades para a nova base de dados de conhecimento.  
  
2.  Selecione **Gerenciamento de Domínio** como a atividade e clique em **Criar** para criar a nova base de dados de conhecimento ou em **Abrir** para abrir uma base de dados de conhecimento existente.  
  
3.  Sobre o **gerenciamento de domínio** clique no **criar um domínio** ícone acima da lista de domínios.  
  
##  <a name="Properties"></a> Definir propriedades do domínio  
  
1.  No **criar domínio** caixa de diálogo, digite um nome exclusivo da base de dados de conhecimento e uma descrição de até 256 caracteres.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre propriedades de domínio, consulte [definir propriedades do domínio](../data-quality-services/set-domain-properties.md).  
  
2.  Do **tipo de dados** selecione um tipo de dados para os valores no domínio. O tipo de dados pode ser **cadeia de caracteres** (o padrão), **data**, **inteiro**, ou **Decimal**.  
  
3.  Selecione **usar valores principais** para especificar que o valor principal em um grupo de sinônimos será gerado em vez de um valor que é sinônimo dele. Cancele a seleção de **Usar Valores Principais** para especificar que cada valor de sinônimo seja gerado em sua forma correta ou corrigida, e não seja substituído pelo valor principal do seu grupo.  
  
4.  Se o tipo de dados for **cadeia de caracteres**, selecione **normalizar a cadeia de caracteres** para remover caracteres especiais nos valores de domínio, o que podem melhorar a probabilidade de correspondências.  
  
5.  Do **formato de saída para** lista suspensa, selecione a formatação que será aplicada quando forem gerados os valores de dados no domínio. A formatação é específica do tipo de dados selecionado na etapa 2, conforme mostrado na lista a seguir:  
  
    -   Para um valor da cadeia de caracteres, você pode especificar que a cadeia de caracteres seja gerada como maiúsculas, minúsculas ou inicial maiúscula.  
  
    -   Para um valor de data, você pode especificar o formato do dia, mês e ano.  
  
    -   Para um valor inteiro, você pode especificar o tipo de máscara de formato a ser aplicado.  
  
    -   Para um valor decimal, você pode especificar a precisão e o tipo de máscara de formato a ser aplicado.  
  
     Selecionando **nenhum** no **formato de saída para** lista suspensa significa que nenhum dos formatos na lista será aplicado.  
  
6.  Se o tipo de dados for **cadeia de caracteres**, no **idioma** lista suspensa, selecione a versão de idioma do verificador ortográfico que você deseja aplicar se você habilitar o verificador ortográfico.  
  
7.  Se o tipo de dados for **cadeia de caracteres**, selecione **Habilitar verificador ortográfico** para executar o verificador ortográfico em todos os valores de cadeia de caracteres ao popular o domínio.  
  
8.  Se o tipo de dados for **cadeia de caracteres**, selecione **Desabilitar algoritmos de erro de sintaxe** para popular o domínio sem verificar os valores de cadeia de caracteres para erros de sintaxe.  
  
9. Clique em **OK**.  
  
10. Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [End the Domain Management Activity](../Topic/End%20the%20Domain%20Management%20Activity.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: após a criação de um domínio  
 Depois que você criar um domínio, poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [executar a descoberta de Conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), ou [criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md).  
  
  