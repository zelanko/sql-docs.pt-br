---
title: Criar um domínio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7d3f751d0547c3b335eb71b55370c8e8cb1e5529
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937907"
---
# <a name="create-a-domain"></a>Criar um domínio
  Este tópico descreve como criar um domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Os valores no domínio são uma representação semântica dos dados em um campo. Para obter mais informações sobre domínios, consulte [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md).  
  
 Há duas maneiras de criar um novo domínio. A primeira é durante a etapa Mapear da atividade de descoberta da base de dados de conhecimento, quando você está no processo de analisar um exemplo de dados para adicionar conhecimento a uma base de dados de conhecimento nova ou existente. A segunda é durante a atividade de gerenciamento de domínio, quando, em vez de alterar um domínio existente, você cria um novo domínio.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Para criar um domínio, você precisa ter criado e aberto uma base de dados de conhecimento.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou o dqs_administrator no banco de dados DQS_MAIN para criar um domínio.  
  
##  <a name="create-a-domain-in-the-knowledge-discovery-activity"></a><a name="Discovery"></a> Criar um domínio na atividade Descoberta da Base de Dados de Conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento** e selecione uma base de dados de conhecimento ou clique em **Nova base de dados de conhecimento** e insira propriedades para a nova base de dados de conhecimento.  
  
3.  Selecione **Descoberta da Base de Dados de Conhecimento** como a atividade e clique em **Criar** para criar a nova base de dados de conhecimento ou em **Abrir** para abrir uma base de dados de conhecimento existente.  
  
4.  Na página **Mapa** , especifique uma conexão com a fonte de dados. Para obter mais informações, consulte [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md).  
  
5.  Na tabela **Mapeamentos** , selecione uma coluna de origem na lista suspensa da coluna **Coluna de Origem** de uma linha vazia. Se não existir um domínio correspondente, clique no ícone **Criar um Domínio** .  
  
##  <a name="create-a-domain-in-the-domain-management-activity"></a><a name="DomainManagement"></a>Criar um domínio na atividade de gerenciamento de domínio  
  
1.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir base de dados de conhecimento** e selecione uma base de dados de conhecimento ou clique em **Nova base de dados de conhecimento** e insira propriedades para a nova base de dados de conhecimento.  
  
2.  Selecione **Gerenciamento de Domínio** como a atividade e clique em **Criar** para criar a nova base de dados de conhecimento ou em **Abrir** para abrir uma base de dados de conhecimento existente.  
  
3.  Na página **Gerenciamento de Domínio** , clique no ícone **Criar um Domínio** acima da lista de domínios.  
  
##  <a name="set-domain-properties"></a><a name="Properties"></a>Definir propriedades de domínio  
  
1.  Na caixa de diálogo **Criar Domínio** , insira um nome que seja exclusivo da base de dados de conhecimento e uma descrição de até 256 caracteres.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre propriedades de domínio, consulte [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).  
  
2.  Na lista **Tipo de Dados** , selecione um tipo de dados para os valores no domínio. O tipo de dados pode ser **Cadeia de Caracteres** (o padrão), **Data**, **Inteiro**ou **Decimal**.  
  
3.  Selecione **Usar Valores Principais** para especificar que o valor principal em um grupo de sinônimos será gerado, e não um valor que é sinônimo dele. Cancele a seleção de **Usar Valores Principais** para especificar que cada valor de sinônimo seja gerado em sua forma correta ou corrigida, e não seja substituído pelo valor principal do seu grupo.  
  
4.  Se o tipo de dados for **Cadeia de Caracteres**, selecione **Cadeia de Caracteres de Normalização** para remover caracteres especiais nos valores de domínio, o que pode melhorar a probabilidade de correspondências.  
  
5.  Na lista suspensa **Formato de Saída para** , selecione a formatação que será aplicada quando forem gerados os valores de dados no domínio. A formatação é específica do tipo de dados selecionado na etapa 2, conforme mostrado na lista a seguir:  
  
    -   Para um valor da cadeia de caracteres, você pode especificar que a cadeia de caracteres seja gerada como maiúsculas, minúsculas ou inicial maiúscula.  
  
    -   Para um valor de data, você pode especificar o formato do dia, mês e ano.  
  
    -   Para um valor inteiro, você pode especificar o tipo de máscara de formato a ser aplicado.  
  
    -   Para um valor decimal, você pode especificar a precisão e o tipo de máscara de formato a ser aplicado.  
  
     Selecionar **Nenhum** na lista suspensa **Formato de Saída para** significa que nenhum dos formatos na lista será aplicado.  
  
6.  Se o tipo de dados for **Cadeia de Caracteres**, na lista suspensa **Idioma** , selecione a versão de idioma do verificador ortográfico a ser aplicada se você habilitar o verificador ortográfico.  
  
7.  Se o tipo de dados for **Cadeia de Caracteres**, selecione **Habilitar Verificador Ortográfico** para executar todos os valores da cadeia de caracteres ao popular o domínio.  
  
8.  Se o tipo de dados for **Cadeia de Caracteres**, selecione **Desabilitar Algoritmos de Erro de Sintaxe** para popular o domínio sem verificar se existem erros de sintaxe em valores da cadeia de caracteres.  
  
9. Clique em **OK**.  
  
10. Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [Terminar a atividade Gerenciamento de Domínio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="follow-up-after-creating-a-domain"></a><a name="FollowUp"></a> Acompanhamento: após a criação de um domínio  
 Depois que você criar um domínio, poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
