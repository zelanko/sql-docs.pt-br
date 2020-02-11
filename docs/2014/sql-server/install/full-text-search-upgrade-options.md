---
title: Opções de atualização da pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- Full-Text Search
- Upgrade options, Full-Text Search
ms.assetid: 16c9376b-5fbb-4495-a429-06a2493849c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 575105d61446f2fd272e4087457e7762c1abb2e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095093"
---
# <a name="full-text-search-upgrade-options"></a>Opções de Atualização da Pesquisa de Texto Completo
  Use a página Opções de Atualização da Pesquisa de Texto Completo do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para selecionar as opções a serem usadas para os bancos de dados que você está atualizando no momento.  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , cada índice de texto completo reside em um catálogo de texto completo que pertence a um grupo de arquivos, tem um caminho físico e é tratado como um arquivo de banco de dados. Agora, um catálogo de texto completo é um conceito lógico – um objeto virtual – que se refere a um grupo de índices de texto completo. Por isso, um novo catálogo de texto completo não é tratado como um arquivo de banco de dados com um caminho físico. No entanto, durante a atualização de qualquer catálogo de texto completo que contém arquivos de dados, é criado um novo grupo de arquivos no mesmo disco. Isso mantém o antigo comportamento de E/S do disco após a atualização. Qualquer índice de texto completo desse catálogo será colocado no novo grupo de arquivos se existir o caminho raiz. Se o caminho do antigo catálogo de texto completo for inválido, a atualização manterá o índice de texto completo no mesmo grupo de arquivos que a tabela base ou, no caso de uma tabela particionada, no grupo de arquivos primário.  
  
## <a name="options"></a>Opções  
 Quando você atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], escolha uma das opções de atualização de texto completo a seguir.  
  
 **Importar**  
 Os catálogos de texto completo são importados. A importação costuma ser consideravelmente mais rápida do que a recompilação. Por exemplo, quando é usada apenas uma CPU, a importação é executada cerca de 10 vezes mais rápido do que a recompilação. Contudo, um catálogo de texto completo importado do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] não usa os separadores de palavras novos e aprimorados, por isso pode ser necessário recompilar o catálogo de texto completo no futuro.  
  
> [!NOTE]  
>  A recompilação pode ser executada no modo multi-threaded e, se houver mais de 10 CPUs disponíveis, ela poderá ser executada mais rápido do que a importação se você permitir que a recompilação use todas as CPUs.  
  
 Se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recompilados. Essa opção está disponível apenas para bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Para obter informações sobre o impacto da importação do índice de texto completo, consulte "Considerações sobre como escolher uma opção de atualização de texto completo", mais adiante neste tópico.  
  
 **Constitui**  
 Os catálogos de texto completo são recompilados usando-se os separadores de palavras novos e aprimorados. A recompilação de índices pode demorar bastante tempo, e uma quantidade significativa de memória e CPU pode ser necessária após a atualização.  
  
 **Definido**  
 Os catálogos de texto completo são redefinidos. Quando atualizados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os arquivos de catálogo de texto completo são removidos, mas os metadados dos catálogos e dos índices de texto completo são preservados. Depois de serem atualizados, todos os índices de texto completo são desabilitados para o controle de alteração e os rastreamentos não são iniciados automaticamente. O catálogo permanecerá vazio até você executar uma população completa manualmente, depois que a atualização for concluída.  
  
 Todas essas opções de atualização asseguram que os bancos de dados atualizados se beneficiem totalmente dos aprimoramentos de desempenho de texto completo.  
  
## <a name="considerations-for-choosing-a-full-text-upgrade-option"></a>Considerações sobre como escolher uma opção de atualização de texto completo  
 Ao escolher a opção de atualização para sua atualização, considere o seguinte:  
  
-   Como você usa os separadores de palavras?  
  
     O serviço de pesquisa de texto completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui separadores de palavras e lematizadores. Eles podem alterar os resultados de consultas de texto completo do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para um cenário ou padrão de texto específico. Portanto, a maneira como você usa os separadores de palavras é importante na hora de escolher uma opção de atualização apropriada:  
  
    -   Se os separadores de palavras do idioma de texto completo que você usa não tiverem sido mudados ou se a precisão dos dados recuperados não for um fator crucial, a importação será a opção adequada. Posteriormente, se você tiver algum problema em relação a recuperação, poderá atualizar para os novos separadores de palavras recompilando os catálogos de texto completo.  
  
    -   Se a precisão dos dados recuperados for um aspecto importante e você usar um dos separadores de palavras que foram adicionados após o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a recompilação será adequada.  
  
-   Algum índice de texto completo foi compilado em colunas de chave de texto completo integer?  
  
     A recompilação faz otimizações internas que, em alguns casos, melhoram o desempenho de consultas do índice de texto completo atualizado. Especificamente, se você tiver catálogos de texto completo que contêm índices de texto completo para os quais a coluna de chave de texto completo da tabela base é do tipo de dados integer, a recompilação atingirá o desempenho ideal de consultas de texto completo depois da atualização. Nesse caso, é altamente recomendável usar a opção **Recriar** .  
  
    > [!NOTE]  
    >  Para os índices de texto completo do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é recomendável que a coluna que funciona como a chave de texto completo seja um tipo de dados integer. Para obter mais informações, consulte [Melhorar o desempenho de índices de texto completo](../../relational-databases/indexes/indexes.md).  
  
-   Qual é a prioridade para colocar a instância de servidor online?  
  
     A importação ou a recompilação durante a atualização usa muitos recursos da CPU, o que faz com que o restante da instância do servidor demore para ser atualizado e ficar online. Se colocar a instância do servidor online o mais rápido possível é importante para você e se você deseja executar uma população manual depois da atualização, a opção **Redefinir** é a mais adequada.  
  
## <a name="additional-resources"></a>Recursos adicionais  
  
