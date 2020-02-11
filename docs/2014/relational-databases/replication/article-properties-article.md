---
title: Propriedades do Artigo – &lt;Artigo&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2903eef63152af9b2e9af1434ba12ea91b4058fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721778"
---
# <a name="article-properties---ltarticlegt"></a>Propriedades do Artigo – &lt;Artigo&gt;
  A caixa de diálogo **Propriedades do Artigo** está disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades de Publicação** . Ela permite exibir e definir propriedades para todos os tipos de artigos. Algumas propriedades só podem ser definidas quando a publicação é criada, e outras só podem ser definidas se a publicação não tiver assinaturas ativas. Propriedades que não podem ser definidas são exibidas como somente leitura.  
  
> [!NOTE]  
>  Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [Alterar propriedade da publicação e do artigo](publish/change-publication-and-article-properties.md).  
  
 Cada propriedade na caixa de diálogo **Propriedades do Artigo** inclui uma descrição. Clique em uma propriedade e sua descrição é exibida na parte inferior da caixa de diálogo. Este tópico fornece informações adicionais sobre várias propriedades. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as publicações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Propriedades que se aplicam a publicações transacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Propriedades que se aplicam a publicações de mesclagem.  
  
-   Propriedades que se aplicam a publicações transacional e de instantâneo de Publicadores Oracle.  
  
## <a name="options-for-all-publications"></a>Opções para todas as publicações.  
 **Copiar esquemas de particionamento de tabela** e **Copiar esquemas de particionamento de índice**  
 O[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] apresentou os particionamentos de tabela e índice, que não têm relação com as ofertas de replicação de particionamento por meio de filtros de linha e coluna. As opções **Copiar esquemas de particionamento de tabela** e **Copiar esquemas de particionamento de índice** especificam se os esquemas de participação devem ser copiados no Assinante. Para obter mais informações sobre particionamento, consulte [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Converter tipos de dados**  
 Determina se tipos de dados definidos pelo usuário devem ou não ser convertidos em tipos de dados base ao criar objetos no Assinante. Os tipos de dados definidos pelo usuário incluem os tipos CLR introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Especifique um valor **True** se você for replicar esses tipos de dados para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; isso assegura que eles possam ser tratados apropriadamente no Assinante.  
  
 **Criar esquemas no Assinante**  
 O[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] apresentou esquemas, que são definidos usando a instrução CREATE SCHEMA. Um esquema é o proprietário de um objeto; é usado em um nome de várias partes, como \<Database>.\<Schema>.\<Object>. Se houver objetos no banco de dados de propriedade de esquemas diferentes de DBO, a replicação pode criar esses esquemas no Assinante para que os objetos publicados sejam criados.  
  
 Se você replicar dados para versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Defina essa opção como **False**, porque versões anteriores não oferecem suporte a CREATE SCHEMA.  
  
-   Para cada esquema, adicione um usuário ao banco de dados de assinatura com o mesmo nome que o esquema.  
  
 **Converter XML em NTEXT**, **Converter tipo de dados MAX em NTEXT e IMAGE**, **Converter o novo datetime em NVARCHAR**, **Converter filestream em tipo de dados MAX**, **Converter CLR grande em tipo de dados MAX**, **Converter hierarchyId em tipo de dados MAX**, e **Converter espacial em tipo de dados MAX**.  
 Determina se os tipos de dados e os atributos devem ser convertidos como descrito. Especifique um valor de **Verdadeiro** se você replicará esses tipos de dados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isto assegura que eles podem ser tratadps corretamente pelo Assinante.  
  
 **Nome do objeto de destino**  
 O nome do objeto criado no banco de dados de assinatura. Essa opção não pode ser alterada para artigos em publicações habilitadas para replicação transacional ponto a ponto.  
  
 **Proprietário do objeto de destino**  
 O esquema no qual o objeto é criado no banco de dados de assinatura. O padrão é o esquema ao qual o objeto pertence no banco de dados de publicação, com as exceções seguintes:  
  
-   Para artigos em publicação de mesclagem com um nível de compatibilidade abaixo de 90: por padrão, o proprietário é deixado em branco e especificado como **dbo** durante a criação do objeto no Assinante.  
  
-   Para artigos em publicações Oracle: por padrão, o proprietário é especificado como **dbo**.  
  
-   Para artigos em publicações que usam instantâneos de modo de caracteres (que são usados para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)] ): por padrão o proprietário é deixado em branco. O proprietário assume o padrão do proprietário associado à conta usada pelo Agente de Distribuição ou Agente de Mesclagem para se conectar ao Assinante.  
  
 Essa opção não pode ser alterada para artigos em publicações habilitadas para replicação transacional ponto a ponto.  
  
 **Gerenciar automaticamente os intervalos de identidades**  
 A replicação, por padrão, gerencia todas as colunas de identidade no Publicador e em cada Assinante. Cada nó de replicação é atribuído a um intervalo de valores de identidade (especificado com as opções **Tamanho do intervalo do Publicador** e **Tamanho do intervalo do Assinante** ) para garantir que um determinando valor só seja usado em um nó. Para obter mais informações, consulte [Replicar colunas de identidade](publish/replicate-identity-columns.md).  
  
## <a name="options-for-transactional-publications"></a>Opções para publicações transacionais.  
 **Copiar procedimentos armazenados INSERT, UPDATE e DELETE**  
 Se na seção **Entrega de Instrução** dessa caixa de diálogo você selecionar o uso de procedimentos armazenados para propagar alterações aos Assinantes (o padrão), selecione se os procedimentos devem ser copiados ou não no Assinante. Se você selecionar **False**, terá de copiar os procedimentos manualmente ou o Agente de Distribuição falhará ao tentar entregar as alterações.  
  
 **Statement delivery**  
 As opções nesta seção se aplicam a todas as tabelas, inclusive exibições indexadas que são replicadas como tabelas. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use as opções padrão, a menos que seu aplicativo exija funcionalidade diferente. Por padrão, a replicação transacional propaga alterações aos Assinantes por um conjunto de procedimentos armazenados instalados em cada Assinante. Quando ocorre uma inserção, atualização ou exclusão em uma tabela no Publicador, a operação é convertida em uma chamada para um procedimento armazenado no Assinante.  
  
 As opções de **entrega de instrução** especificam se deve ou não ser usado um procedimento armazenado e, se for usado, qual formato deve ser usado para parâmetros passados ao procedimento. As opções de **procedimento armazenado** permitem que você use os procedimentos que a replicação cria automaticamente ou substitua procedimentos armazenados criados.  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **Replicar**  
 Essa opção só se aplica a procedimentos armazenados. Determina se a definição do procedimento armazenado (a instrução CREATE PROCEDURE) ou sua execução devem ser replicadas ou não. Se você replicar a execução do procedimento, a definição do procedimento será replicada para o Assinante quando a assinatura for inicializada; quando o procedimento armazenado for executado no Publicador, a replicação executará o procedimento correspondente no Assinante. Isso pode fornecer um desempenho significativamente melhor em casos onde são executadas grandes operações em lote. Para obter mais informações, consulte [Publicando execução de procedimento armazenado em replicação transacional](transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="options-for-merge-publications"></a>Opções para publicações de mesclagem  
 A caixa de diálogo **Propriedades do Artigo** para publicações de mesclagem tem duas guias: **Propriedades** e **Resolvedor**.  
  
### <a name="properties-tab"></a>Guia Propriedades  
 **Direção de sincronização**  
 Determina se as alterações podem ser carregadas de Assinantes que usam tipo de assinatura de cliente:  
  
-   **Bidirecional** (o padrão): as alterações podem ser baixadas no Assinante e carregadas no Publicador.  
  
-   **Download somente para Assinante, proibir alterações do Assinante**: as alterações podem ser baixadas no Assinante, mas não podem ser carregadas no Publicador. Os gatilhos impedem que sejam feitas alterações no Assinante.  
  
-   **Download somente para Assinante, permitir alterações do Assinante**: as alterações podem ser baixadas no Assinante, mas não podem ser carregadas no Publicador.  
  
 Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Opções de partição**  
 Especifica o tipo de partição criado por um filtro com parâmetros. Para obter mais informações, consulte a seção "Configurando opções de partição" em [Filtros de linha com parâmetros](merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Nível de rastreamento**  
 Determina se as alterações para a mesma linha ou para a mesma coluna devem ser tratadas como um conflito.  
  
 **Verificar permissão de INSERT**, **Verificar permissão de UPDATE**e **Verificar permissão de DELETE**  
 Determina se verificar ou não durante a sincronização se o logon do Assinante tem as permissões INSERT, UPDATE ou DELETE nas tabelas publicadas, no banco de dados de publicação. O padrão é **False** porque replicação de mesclagem não requer que essas permissões sejam concedidas; o acesso às tabelas publicadas é controlado pela PAL (Lista de Acesso à Publicação). Para obter mais informações sobre a PAL, consulte [Secure the Publisher](security/secure-the-publisher.md) (Proteger o publicador).  
  
 Você pode requerer que as permissões sejam verificadas se quiser permitir que um ou mais Assinantes carreguem algumas alterações de dados publicados, mas não outras. Por exemplo, você pode adicionar um Assinante a PAL, mas não conceder ao Assinante nenhuma permissão nas tabelas do banco de dados de publicação. Depois você pode definir Verificar permissões DELETE como **True**: o Assinante poderá carregar inserções e atualizações, mas não exclusões.  
  
 **UPDATE multicolunas**  
 Quando a replicação de mesclagem efetua uma atualização, todas as colunas alteradas em uma instrução UPDATE são atualizadas e colunas inalteradas são redefinidas ao seu valor original. A alternativa nesses casos é emitir várias instruções UPDATE, com uma instrução UPDATE para cada coluna alterada. A instrução UPDATE multicolunas é geralmente mais eficiente, mas você deve considerar definir a opção como **False** se os gatilhos da tabela tiverem sido definidos para responder a atualizações de determinadas colunas e se eles responderem inadequadamente devido a essas colunas serem redefinidas quando ocorre a atualização.  
  
> [!IMPORTANT]  
>  Essa opção é preterida e será removida em uma versão futura.  
  
### <a name="resolver-tab"></a>Guia Resolvedor  
 **Usar o resolvedor padrão**  
 Se você selecionar o resolvedor padrão, os conflitos serão resolvidos com base na prioridade atribuída a cada Assinante ou na primeira alteração gravada no Publicador, dependendo do tipo de assinatura usado. Para obter mais informações, consulte [Detectar e resolver conflitos de replicação de mesclagem](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 **Usar um resolvedor personalizado (registrado no Distribuidor)**  
 Se você escolher usar um resolvedor de artigo (um fornecido pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um que você gravou), deve selecionar um resolvedor na caixa de listagem. Para obter mais informações, consulte [Replicação de mesclagem avançada – detecção e resolução de conflito](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Se o resolvedor requerer uma entrada, especifique-a na caixa de texto **Insira as informações necessárias para o desenvolvedor** . Para obter mais informações sobre entrada requerida por resolvedores personalizados [!INCLUDE[msCoName](../../includes/msconame-md.md)] , consulte [Resolvedores Microsoft baseados em COM](merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 **Permitir que o Assinante resolva conflitos interativamente durante a sincronização sob demanda**  
 Selecione essa opção se o Assinante for usar sincronização sob demanda (o padrão em replicação de mesclagem) e você quiser resolver os conflitos interativamente. Especifique sincronização sob demanda na página **Agenda de Sincronização** do Assistente para Nova Assinatura. Para resolver conflitos interativamente, use a interface do usuário Resolvedor Interativo. Para obter mais informações, consulte [Resolução de conflito interativo](merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Requer verificação de uma assinatura digital antes da mesclagem**  
 Todos os resolvedores com base em COM fornecidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] são assinados. Selecione essa opção para verificar se o resolvedor é válido na sincronização.  
  
## <a name="options-for-oracle-publications"></a>Opções para publicações Oracle  
 A caixa de diálogo **Propriedades do Artigo** para publicações Oracle tem duas guias: **Propriedades** e **Mapeamento de Dados**. Publicações Oracle não oferecem suporte a todas as propriedades que as publicações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem. Para obter mais informações, consulte [Considerações de design e limitações para Publicadores Oracle](non-sql/design-considerations-and-limitations-for-oracle-publishers.md)  
  
### <a name="properties-tab"></a>Guia Propriedades  
 **Copiar procedimentos armazenados INSERT, UPDATE e DELETE**  
 Se o artigo estiver em uma publicação transacional, na seção **Entrega de Instrução** dessa caixa de diálogo, você seleciona o uso de procedimentos armazenados para propagar alterações nos Assinantes (o padrão) e seleciona se os procedimentos devem ser copiados ou não no Assinante. Se você selecionar **False**, terá de copiar os procedimentos manualmente ou o Agente de Distribuição falhará ao tentar entregar as alterações.  
  
 **Proprietário do objeto de destino**  
 Se você inserir um valor diferente de **dbo**:  
  
-   Para Assinantes que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve assegurar que seja criado um esquema no Assinante com o mesmo nome do valor inserido. Para obter mais informações, veja [CREATE SCHEMA &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
-   Para Assinantes que executam versões anteriores do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], para cada esquema adicione um usuário ao banco de dados de assinatura, com o mesmo nome do esquema.  
  
 **Nome do espaço de tabela**  
 O espaço de tabela no qual criar as tabelas de controle de alteração de replicação na instância do servidor Oracle. Para obter mais informações, consulte [Gerenciar espaços de tabela Oracle](non-sql/manage-oracle-tablespaces.md).  
  
 **Statement delivery**  
 As opções nesta seção se aplicam a todas as tabelas em publicações transacionais. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use as opções padrão, a menos que seu aplicativo exija funcionalidade diferente. Por padrão, a replicação transacional propaga alterações aos Assinantes por um conjunto de procedimentos armazenados instalados em cada Assinante. Quando ocorre uma inserção, atualização ou exclusão em uma tabela no Publicador, a operação é convertida em uma chamada para um procedimento armazenado no Assinante.  
  
 As opções de **entrega de instrução** especificam se deve ou não ser usado um procedimento armazenado e, se for usado, qual formato deve ser usado para parâmetros passados ao procedimento. As opções de **procedimento armazenado** permitem que você use os procedimentos que a replicação cria automaticamente ou substitua procedimentos armazenados criados.  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="data-mapping-tab"></a>Guia Mapeamento de Dados  
 **Nome da coluna**  
 O nome da coluna no Publicador (somente leitura).  
  
 **Tipo de dados do Publicador**  
 O tipo de dados Oracle para a coluna no Publicador (somente leitura). O tipo de dados só pode ser alterado diretamente no banco de dados Oracle. Para obter mais informações, consulte a documentação Oracle.  
  
 **Tipo de dados de Assinante**  
 O tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual o tipo de dados Oracle é mapeado quando os dados são replicados:  
  
-   Para alguns tipos de dados, há somente um mapeamento possível; em tal caso, a coluna na grade de propriedades é somente leitura.  
  
-   Para alguns tipos, é possível selecionar mais de uma opção. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use o mapeamento padrão, a menos que seu aplicativo exija um mapeamento diferente. Para obter mais informações, consulte [Mapeamento de tipo de dados para Publicadores Oracle ](non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)   
 [Reinicializar uma assinatura](reinitialize-a-subscription.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  
