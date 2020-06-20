---
title: Definir propriedades de domínio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.domainproperties.f1
ms.assetid: 8a3c88ca-31d6-4f75-9aca-cf027c6d9845
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3a68ba77473775aecb0cc73e0c4415fed0e5835d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937397"
---
# <a name="set-domain-properties"></a>Definir propriedades do domínio
  Este tópico descreve como definir propriedades de domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Para definir propriedades para um domínio, você precisa criar uma base de dados de conhecimento e um domínio.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para definir propriedades em um domínio.  
  
##  <a name="set-domain-properties"></a><a name="Set"></a>Definir propriedades de domínio  
  
1.  Defina as propriedades em um domínio existente abrindo uma base de dados de conhecimento na atividade Gerenciamento de Domínio (consulte [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md)) e selecione o domínio apropriado na lista **Domínios** . A página Propriedades de Domínio será exibida por padrão.  
  
2.  Defina as propriedades em um novo domínio depois de criá-la conforme descrito em [Create a Domain](../../2014/data-quality-services/create-a-domain.md).  
  
3.  Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [Terminar a atividade Gerenciamento de Domínio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="follow-up-after-setting-domain-properties"></a><a name="FollowUp"></a>Acompanhamento: depois de definir propriedades de domínio  
 Após definir propriedades de domínio, você poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="domain-properties"></a><a name="Properties"></a>Propriedades do domínio  
  
###  <a name="domain-name-and-description"></a><a name="Name"></a>Nome e descrição do domínio  
 Quando um domínio é criado, o nome ou a descrição do domínio pode ser alterado. O nome do domínio deve ser exclusivo para a base de dados de conhecimento. A descrição pode ter até 256 caracteres.  
  
###  <a name="data-type"></a>Tipo de dados <a name="Type"></a>  
 Quando você criar o domínio, selecione um dos tipos de dados a seguir para obter os valores no domínio: **Cadeia de Caracteres** (o padrão), **Data**, **Inteiro**ou **Decimal**. Depois de criar o domínio, você poderá exibir o tipo de dados, mas não poderá alterá-lo O tipo de dados selecionado para um domínio define o tipo de dados de origem que pode ser mapeado para o domínio. Para obter informações sobre tipos de dados com suporte em cada um dos quatro tipos de dados de domínio no DQS, consulte [Tipos de dados do SQL Server e do SSIS com suporte para domínios do DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
###  <a name="use-leading-values"></a><a name="Leading"></a>Usar valores principais  
 Marque esta caixa de seleção para especificar que o valor principal em um grupo de sinônimos será gerado, e não um valor que é sinônimo dele. Cancele a seleção de **Usar Valores Principais** para especificar que cada valor de sinônimo seja gerado em sua forma correta ou corrigida, e não seja substituído pelo valor principal do seu grupo.  
  
###  <a name="normalize-string"></a><a name="Normalize"></a>Normalizar cadeia de caracteres  
 Se o tipo de dados for **String**, clique para ignorar os caracteres especiais nos dados de origem para o processamento da qualidade de dados pelo DQS. O DQS substitui internamente os caracteres especiais com nulo ou um espaço quando os dados forem carregados no domínio. Um caracteres de dois-pontos, hífen, ponto, aspas duplas ou ponto-e-vírgula é substituído por um espaço. Um caracteres de aspas simples é substituído por um nulo. O uso do nulo associa as duas partes da cadeia de caracteres.  
  
 Ignorar os caracteres especiais em um valor da cadeia de caracteres pode aumentar a precisão da correspondência. A pontuação de similaridade entre duas cadeias de caracteres pode ser aumentada, substituindo caracteres especiais por um nulo ou um espaço. Marcas de pontuação ou outros símbolos têm grande probabilidade de serem diferentes em cadeias de caracteres diferentes. A substituição interna de caracteres especiais pode permitir que a pontuação ultrapasse o limite mínimo de correspondência no DQS, levando duas cadeias de caracteres a serem consideradas correspondentes, quando, do contrário, isso não ocorreria. Entretanto, a opção por ignorar caracteres especiais poderá depender do tipo de dados no qual você está executando a correspondência. Por exemplo, quando você estiver trabalhando com dados no Sistema de medidas em inglês, ignorar as aspas duplas e aspas simples em dados do produto poderá resultar em falsos positivos se uma aspa dupla representar uma polegada e uma aspa simples representar uma medida em pés.  
  
 A normalização é executada quando dados são carregados e indexados nas fases de processamento de dados de descoberta, política de correspondência, projeto de correspondência e atividades de projeto de limpeza. Se habilitada, a normalização e a transformação de relações baseada em termos serão ambas realizadas em uma fase de pré-processamento antes da análise. Elas são executados em cada domínio antes de qualquer algoritmo ser aplicado que compute a semelhança entre cadeias de caracteres. Se a análise de domínio composto for solicitada, ela será executada antes da transformação na normalização e nas relações baseadas em termos, pois a análise de delimitador requer símbolos. Outras operações, como regras de domínio e alterações de valor de domínio, serão executadas depois das transformações. Os dados resultantes não são alterados pela substituição interna de caracteres especiais no DQS.  
  
###  <a name="format-output-to"></a><a name="Format"></a>Formatar saída para  
 Selecione a formatação que será aplicada quando forem gerados os valores de dados no domínio. A formatação é específica do tipo de dados selecionado, conforme mostrado na lista a seguir. Selecionar **Nenhum** significa que nenhum formato da lista será aplicado.  
  
-   Para um valor da cadeia de caracteres, você pode especificar que a cadeia de caracteres seja gerada como maiúsculas, minúsculas ou inicial maiúscula.  
  
-   Para um valor de data, você pode especificar o formato do dia, mês e ano.  
  
-   Para um valor inteiro, você pode especificar o tipo de máscara de formato a ser aplicado.  
  
-   Para um valor decimal, você pode especificar a precisão e o tipo de máscara de formato a ser aplicado.  
  
###  <a name="language"></a><a name="Language"></a>Idioma  
 Se o tipo de dados for **Cadeia de Caracteres**, selecione o idioma a ser associado ao domínio para a operação do verificador ortográfico. Esta seleção só se aplica ao verificador ortográfico, pois os resultados do verificador ortográfico dependem do idioma em uso. A seleção se aplica apenas a um único domínio com um tipo de dados cadeia de caracteres. A propriedade de idioma não é relevante para domínios compostos. O idioma para cada parte de um domínio composto é determinado pelo único domínio relevante.  
  
 Inglês é o idioma padrão. A definição da propriedade **Idioma** como **Outro** desabilita o verificador ortográfico para o domínio.  
  
> [!TIP]  
>  Se o idioma não for exibido na lista suspensa **Idioma** , selecione **Outro**. Isso garante que o DQS limpe e elimine duplicatas para os dados de idiomas não listados com base no conhecimento disponível (regras de domínio, valores de domínio, TBRs, regra de correspondência) no domínio.  
  
###  <a name="enable-speller"></a><a name="Speller"></a>Habilitar verificador ortográfico  
 Se o tipo de dados for **Cadeia de Caracteres**, clique para habilitar o verificador ortográfico do DQS para o domínio. O verificador ortográfico só funciona em domínios com um tipo de dados cadeia de caracteres. A caixa de seleção **Habilitar Verificador Ortográfico** habilita o verificador ortográfico apenas para o único domínio associado com a caixa de seleção. A caixa de seleção não se aplica a um domínio composto.  
  
 O verificador ortográfico propõe correções de sintaxe e validação em valores no domínio. Para obter mais informações, consulte [Use the DQS Speller](../../2014/data-quality-services/use-the-dqs-speller.md).  
  
###  <a name="disable-syntax-error-algorithms"></a><a name="Syntax"></a>Desabilitar algoritmos de erro de sintaxe  
 Se o tipo de dados for **Cadeia de Caracteres**, selecione para especificar que erros de sintaxe não sejam identificados pelo DQS no domínio durante a limpeza. Marque esta caixa de seleção quando a identificação de erros de sintaxe para esse domínio for irrelevante. Por exemplo, a identificação de erros de sintaxe pode não ter importância para um número de série. Este controle só está disponível para o tipo de dados cadeia de caracteres. O DQS não verificará se existem erros de sintaxe em tipos de dados que não sejam cadeia de caracteres.  
  
  
