---
title: Anexar um domínio ou domínio de composição aos dados de referência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.refdata.f1
- sql12.dqs.dm.refcatalog.f1
ms.assetid: 36af981c-d0d0-4dc6-afe5-bbb3c97845dc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 74554e305dbbeb736eba3d8379c7f6569e56d333
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154508"
---
# <a name="attach-a-domain-or-composite-domain-to-reference-data"></a>Anexar domínio ou domínio de composição a dados de referência
  Este tópico descreve como anexar domínios/domínios compostos em uma base de conhecimento de qualidade de dados a um serviço de dados de referência no Azure Marketplace para criar conhecimento em relação aos dados de referência de alta qualidade. Cada serviço de dados de referência contém um esquema (colunas de dados). Após anexar um domínio ou um domínio composto a um serviço de dados de referência, mapeie o domínio anexado ou os domínios individuais no domínio composto anexado para as colunas apropriadas em um esquema de serviço de dados de referência. Ao anexar um domínio composto a um serviço de dados de referência, você pode anexar apenas um domínio a um serviço de dados de referência e, em seguida, mapear os domínios individuais no domínio composto para as colunas apropriadas no esquema de serviço de dados de referência.  
  
> [!WARNING]  
>  O domínio composto anexado a um serviço de dados de referência está disponível na lista suspensa dos domínios ao mapear domínios para colunas no esquema de serviço de dados de referência. Não mapeie o domínio composto para uma coluna no esquema do serviço de dados de referência; mapeie apenas domínios individuais em um domínio composto para as colunas apropriadas no esquema de serviço de dados de referência. Caso contrário, isso resultará em um erro.  
  
 Um esquema de serviço de dados de referência pode ter uma coluna obrigatória que deverá ser mapeada com o domínio apropriado se você optar por usar o serviço de dados de referência. A coluna obrigatória em um esquema de dados de referência é identificada com "(M)" no nome da coluna. Por exemplo, **AddressLine** é a coluna de esquema obrigatória em **Melissa Data – Dados de Endereço** e **CompanyName** é a coluna de esquema obrigatória em **Digital Trowel Inc. – Dados de empresas norte-americanas e de profissionais para usuários do SQL**.  
  
 Neste tópico, criaremos quatro domínios: **Linha de endereço**, **Cidade**, **Estado** e **CEP**, em um domínio composto, **Verificação de Endereço**, anexaremos o domínio composto para o serviço de dados de referência de **Melissa Data – Dados de Endereço** e mapearemos os domínios individuais no domínio composto para as colunas no esquema de serviço de dados de referência.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você deve configurar o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para usar serviços de dados de referência. Consulte [Configurar o DQS para usar dados de referência](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md).  
  
###  <a name="Security"></a> Segurança  
  
#### <a name="permissions"></a>Permissões  
 Você deve ter a função dqs_kb_editor no banco de dados DQS_MAIN para mapear domínios para os dados de referência.  
  
##  <a name="Map"></a>Mapear domínios para dados de referência de Melissa data  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , em **Gerenciamento da Base de Dados de Conhecimento**, clique em **Nova base de dados de conhecimento**.  
  
3.  Na tela **Nova base de dados de conhecimento** , digite um nome para a nova base de dados de conhecimento, clique na atividade **Gerenciamento de Domínio** e clique em **Criar**.  
  
4.  Na tela **Gerenciamento de Domínio** , clique no ícone **Criar um domínio** para criar um domínio. Crie os quatro domínios a seguir: **Linha de Endereço**, **Cidade**, **Estado**e **CEP**.  
  
5.  Clique no ícone **Criar um domínio composto** para criar um domínio composto. Na caixa de diálogo **Criar um domínio composto** , digite **Verificação de Endereço** na caixa **Nome de Domínio Composto** e inclua todos os domínios criados na etapa 3 no domínio composto. Clique em **OK**.  
  
6.  No painel **Domínio** no lado esquerdo, selecione o domínio composto clicando em **Verificação de Endereço**e clique na guia **Dados de Referência** à direita.  
  
7.  Clique no ícone **Procurar** .  
  
8.  Caixa de diálogo **Catálogo de Provedores de Dados de Referência Online** :  
  
    1.  Em **DataMarket Data Quality Services**, selecione a caixa **Melissa Data – Verificação de Endereço**.  
  
    2.  Mapeie as colunas do serviço de dados de referência de Melissa Data – Verificação de Endereço com os domínios apropriados (Linha de Endereço, Cidade, Estado e CEP). Você mapeia as colunas selecionando uma coluna de serviço de dados de referência na coluna **Esquema RDS** e, depois, selecionando o domínio apropriado na coluna **Domínio** . Para adicionar mais linhas à tabela, clique no ícone **Adicionar Entrada de Esquema** .  
  
    3.  Clique em **OK** para salvar as alterações e fechar a caixa de diálogo **Catálogo de Provedores de Dados de Referência Online** .  
  
         ![Caixa de diálogo Catálogo de Provedores de Dados de Referência Online](../../2014/data-quality-services/media/dqs-onlinereferencedataproviderscatalog.gif "Caixa de diálogo Catálogo de Provedores de Dados de Referência Online")  
  
        > [!NOTE]  
        >  -   Na caixa de diálogo **Catálogo de provedores de dados de referência online** , o nó **Data Quality Services do DataMarket** exibe todos os provedores de serviço de dados de referência que você assinou no Azure Marketplace. Se você tiver configurado provedores diretos de serviço de dados de referência online terceirizados no DQS, eles aparecerão em outro nó chamado **Provedores Online Diretos Terceirizados** (não disponível agora, pois nenhum provedor direto de serviço de dados de referência online terceirizado está configurado no DQS).  
  
9. Você retornará à guia **dados de referência** . Na área **configurações do provedor** , altere os valores nas seguintes caixas, se necessário:  
  
    -   **Limite de correção automática**: as correções do serviço de dados de referência com o nível de confiança acima desses valores de limite serão feitas automaticamente. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, insira 0,9 para 90%.  
  
    -   **Candidatos sugeridos**: número de candidatos sugeridos para exibição do serviço de dados de referência.  
  
    -   **Confiança mínima**: as sugestões do serviço de dados de referência com nível de confiança inferior a esse valor serão ignoradas. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, insira 0,6 para 60%.  
  
10. Clique em **Concluir** para publicar a base de dados de conhecimento. Uma mensagem de confirmação aparece depois que a base de dados de conhecimento é publicada com êxito.  
  
 Agora você pode usar essa base de dados de conhecimento para a atividade de limpeza em um projeto de qualidade de dados para padronizar e limpar os endereços dos EUA em seus dados de origem com base no conhecimento fornecido por Melissa data por meio do Azure Marketplace.  
  
##  <a name="FollowUp"></a>Acompanhamento: depois de mapear um domínio para dados de referência  
 Crie um projeto de qualidade de dados e execute a atividade de limpeza na fonte de dados que contém endereços americanos, comparando-a com a base de dados de conhecimento criada neste tópico. Consulte [Limpar dados usando o conhecimento &#40;externo&#41; dos dados de referência](../../2014/data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Serviços de dados de referência no DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)   
 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)  
  
  
