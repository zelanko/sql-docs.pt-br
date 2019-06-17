---
title: Modos de armazenamento e processamento de partição | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- hybrid OLAP
- data storage [Analysis Services]
- relational OLAP
- multidimensional OLAP
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- HOLAP
- MOLAP
- ROLAP
ms.assetid: 86d17547-a0b6-47ac-876c-d7a5b15ac327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74f53ddb6e7e3fc6b9d14ddcc726c2766a598860
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727572"
---
# <a name="partition-storage-modes-and-processing"></a>Modos e processamento de armazenamento de partição
  O modo de armazenamento de uma partição afeta o desempenho de consulta e processamento, requisitos de armazenamento e locais de armazenamento da partição e seu grupo de medidas e cubo pai. A escolha do modo de armazenamento também afeta escolhas de processamento.  
  
 Uma partição pode usar um de três modos de armazenamento básicos:  
  
-   OLAP multidimensional (MOLAP)  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP híbrido (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a todos os três modos de armazenamento básicos. Ele também oferece suporte o cache pró-ativo, que permite combinar as características do armazenamento ROLAP e MOLAP para desempenho de dados e de consulta imediato. Para obter mais informações, consulte [Cache pró-ativo &#40;Partições&#41;](partitions-proactive-caching.md).  
  
## <a name="molap"></a>MOLAP  
 O modo de armazenamento MOLAP faz com que as agregações da partição e uma cópia dos dados de origem sejam armazenados em uma estrutura multidimensional no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando a partição for processada. Essa estrutura MOLAP é altamente otimizada para maximizar o desempenho de consulta. O local de armazenamento pode ser o computador onde a partição foi definida ou em outro computador executando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Como uma cópia dos dados fonte reside na estrutura multidimensional, as consultas podem ser resolvidas sem acessar os dados de origem da partição. Os tempos de resposta de consulta podem ser diminuídos substancialmente usando agregações. Os dados na estrutura MOLAP da partição são apenas atuais como o mais recente processamento da partição.  
  
 Conforme os dados de origem mudam, os objetos no armazenamento MOLAP devem ser processados periodicamente para incorporar essas alterações e torná-los disponíveis aos usuários. O processamento atualiza os dados na estrutura MOLAP completa ou incrementalmente. O tempo entre um processamento e o próximo, cria um período de latência durante o qual os dados nos objetos OLAP podem não corresponder aos dados de origem. Você pode atualizar objetos incremental ou completamente no armazenamento MOLAP sem tornar a partição ou o cubo offline. Entretanto, há situações que podem requerer que você torne o cubo offline para processar determinadas alterações estruturais em objetos OLAP. Você pode minimizar o tempo de inatividade necessário para atualizar o armazenamento MOLAP, atualizando e processando cubos em um servidor temporário e usando a sincronização de banco de dados para copiar os objetos processados para o servidor de produção. Você também pode usar o cachê pró-ativo para minimizar a latência e maximizar a disponibilidade tirando vantagem do desempenho do armazenamento MOLAP. Para obter mais informações, consulte [pró-ativos &#40;partições&#41;](partitions-proactive-caching.md), [sincronizar o Analysis Services Databases](../multidimensional-models/synchronize-analysis-services-databases.md), e [objeto de modelo Multidimensional processamento](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 O modo de armazenamento ROLAP faz com que as agregações da partição sejam armazenadas em exibições indexadas no banco de dados relacional especificado na fonte de dados da partição. Diferentemente do modo de armazenamento MOLAP, o ROLAP não faz com que uma cópia dos dados fonte seja armazenada nas pastas de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em vez disso, quando os resultados não podem ser derivados do cache de consulta, as exibições indexadas na fonte de dados são acessadas para responder as consultas. Resposta da consulta é geralmente mais lenta com o armazenamento ROLAP que os modos MOLAP ou HOLAP. Geralmente, o tempo de processamento é também mais lento no ROLAP. Entretanto, o ROLAP permite que os usuários exibam os dados em tempo real e economizem espaço de armazenamento ao trabalharem com grandes conjuntos de dados consultados raramente, como os dados puramente históricos.  
  
> [!NOTE]  
>  Ao usar o ROLAP, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode retornar informações incorretas relacionadas ao membro desconhecido se uma junção for combinada a uma cláusula GROUP BY. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina erros de integridade relacional em vez de retornar o valor do membro desconhecido.  
  
 Se a partição usar o modo de armazenamento ROLAP e seus dados de origem forem armazenados em [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará criar as exibições indexadas para conter agregações da partição. Se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não puderem criar exibições indexadas, não serão criadas as tabelas de agregação. Embora [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] trate dos requisitos da sessão para criação de exibições indexadas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], as seguintes condições devem ser atendidas pela partição ROLAP e as tabelas em seu esquema para que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crie exibições indexadas para agregações:  
  
-   A partição não pode conter medidas que usam as funções de agregação `Min` ou `Max`.  
  
-   Cada tabela no esquema da partição de ROLAP deve ser usada só uma vez. Por exemplo, o esquema não pode conter [dbo]. [endereço] AS "Customer Address" e [dbo]. [endereço] AS "SalesRep Address".  
  
-   Cada tabela deve ser uma tabela, não uma exibição.  
  
-   Todos os nomes de tabela no esquema da partição devem ser qualificados com o nome de proprietário, por exemplo, [dbo]. [cliente].  
  
-   Todas as tabelas no esquema da partição devem ter o mesmo proprietário, por exemplo, você não pode ter uma cláusula FROM que faz referência às tabelas [tk].[cliente], [john].[armazenamento] e [dave].[vendas_fato_2004].  
  
-   As colunas de fonte das medidas da partição não devem ser anuláveis.  
  
-   Devem ter sido criadas todas as tabelas usadas na exibição com as seguintes opções definidas como ON:  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   O tamanho total da chave de índice no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode exceder 900 bytes. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] declarará essa condição com base nas colunas de chave de comprimento fixo quando a instrução CREATE INDEX for processada. No entanto, se houver colunas de comprimento variável na chave de índice, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] também declarará essa condição para todas as atualizações para as tabelas base. Como agregações diferentes possuem definições de exibição diferentes, o processamento ROLAP, usando exibições indexadas pode ser bem-sucedido ou falhar dependendo do projeto da agregação.  
  
-   A sessão que cria a exibição indexada deve ter as seguintes opções definidas como ON: ARITHABORT, CONCAT_NULL_YEILDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING e ANSI_WARNING. Essa configuração pode ser feita no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   A sessão que cria a exibição indexada deve ter a seguinte opção definida como OFF: NUMERIC_ROUNDABORT. Essa configuração pode ser feita no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="holap"></a>HOLAP  
 O modo de armazenamento HOLAP combina atributos de MOLAP e ROLAP. Como o MOLAP, HOLAP faz com que as agregações da partição a ser armazenado em uma estrutura multidimensional em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. O HOLAP não faz com que uma cópia dos dados fonte seja armazenada. Para consultas que só acessam dados resumidos nas agregações de uma partição, o HOLAP é o equivalente do MOLAP. Consultas que acessam dados de origem-por exemplo, se você quiser fazer drill down até uma célula de cubo atômico para que não há nenhuma agregação dados, deve recuperar dados do banco de dados relacional e não será tão rápido quanto eles seriam se a fonte de dados foram armazenados no structur MOLAP e. Com o modo de armazenamento HOLAP, os usuários geralmente experimentam diferenças substanciais nos tempos de consulta dependendo de se a consulta pode ser resolvida a partir das agregações de cache versus a partir dos próprios dados de origem.  
  
 As partições armazenadas como HOLAP são menores que as partições MOLAP equivalentes, pois elas não contêm dados de origem e respondem mais rapidamente que as partições ROLAP para consultas envolvendo dados resumidos. O modo de armazenamento HOLAP é geralmente adequado a partições em cubos que requerem resposta rápida a consultas de resumos com base em uma grande quantidade de dados de origem. Entretanto, quando os usuários geram consultas que atingem os dados no nível folha, como ao calcular valores de média, o MOLAP geralmente é a melhor escolha.  
  
## <a name="see-also"></a>Consulte também  
 [Cache pró-ativo &#40;partições&#41;](partitions-proactive-caching.md)   
 [Sincronizar bancos de dados do Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)   
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](partitions-analysis-services-multidimensional-data.md)  
  
  
