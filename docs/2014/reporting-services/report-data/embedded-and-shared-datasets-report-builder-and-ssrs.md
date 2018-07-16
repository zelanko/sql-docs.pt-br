---
title: Conjuntos de dados inseridos e compartilhados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: adc95cc0-d15a-413d-bc5a-302eab37a069
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: edc733435dfa55c076a6d37cd95411764996d943
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317916"
---
# <a name="embedded-and-shared-datasets-report-builder-and-ssrs"></a>Conjuntos de dados inseridos e compartilhados (Construtor de Relatórios e SSRS)
  Em um relatório, um conjunto de dados representa dados de relatório retornados em virtude da execução de um consulta em uma fonte de dados externa. O conjunto de dados depende da conexão de dados que contém informações sobre a fonte de dados externa. Os dados em si não são incluídos na definição de relatório. O conjunto de dados contém um comando de consulta, uma coleção de campos, parâmetros, filtros e opções de dados que incluem diferenciação de maiúsculas e minúsculas e agrupamento. Existem dois tipos de conjuntos de dados:  
  
-   **Conjuntos de dados compartilhados.** Um conjunto de dados compartilhado é publicado em um servidor de relatório e pode ser usado por vários relatórios. Um conjunto de dados compartilhado deve ser baseado em uma fonte de dados compartilhada. Um conjunto de dados compartilhado pode ser armazenado em cache e programado, criando um plano de atualização do cache.  
  
-   **Conjuntos de dados inseridos.** Os conjuntos de dados inseridos são definidos e usados por um único relatório.  
  
 A diferença entre os dois está no modo como são criados, armazenados e gerenciados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="shared-datasets"></a>Conjuntos de dados compartilhados  
 Use um conjunto de dados compartilhado para fornecer uma consulta que pode ser usada por mais de um relatório. Os conjuntos de dados compartilhados são armazenados no servidor de relatório e gerenciados separadamente dos relatórios ou das fontes de dados compartilhadas. Por exemplo, um administrador de servidor de relatório pode atualizar a consulta para tirar proveito da indexação aprimorada ou de outra otimização de desempenho de consulta.  
  
 Recomendamos usar conjuntos de dados compartilhados o máximo possível. Você pode otimizar uma consulta ou armazenar em cache resultados da consulta para tirar proveito do desempenho do relatório. Os conjuntos de dados compartilhados facilitam o gerenciamento do acesso a dados e ajudam a manter os relatórios e os conjuntos de dados acessados mais seguros e mais funcionais.  
  
 No Designer de Relatórios, você pode criar conjuntos de dados compartilhados como parte de um projeto de relatório e controlar se deve implantá-los em um servidor de relatório. Não é possível navegar até um servidor de relatório e selecionar um conjunto de dados compartilhado para adicionar ao seu relatório.  
  
 No Construtor de Relatórios, você pode fazer o seguinte:  
  
1.  Para criar um conjunto de dados compartilhado, use o modo de exibição Design de Conjunto de Dados Compartilhado. É possível salvá-lo em um servidor de relatório ou site do SharePoint para compartilhar com outros relatórios. Você também pode navegar até o servidor de relatório e editar um conjunto de dados compartilhado existente. Nesta exibição, você pode criar uma consulta e definir todas as opções de conjunto de dados. Para obter mais informações, consulte [Modo de exibição de design de conjunto de dados compartilhado &#40;Construtor de Relatórios&#41;](../report-builder/shared-dataset-design-view-report-builder.md).  
  
2.  Para adicionar um conjunto de dados compartilhado a um relatório, abra o Construtor de Relatórios no Modo Design do Relatório. De um assistente ou do painel de dados do relatório, vá para o servidor de relatório e selecione o conjunto de dados compartilhado para adicionar seu relatório. Nesta exibição, você não pode alterar a consulta, exceto para adicionar campos. Você pode substituir outras opções de dados e adicionar filtros. Você não pode remover filtros.  
  
3.  A tabela a seguir compara as propriedades que podem ser configuradas para a definição do conjunto de dados compartilhado no servidor de relatório e a instância do conjunto de dados compartilhado na definição de relatório.  
  
    |Propriedade|Observações sobre a configuração para a definição|Observações sobre a configuração para a instância|  
    |--------------|--------------------------------------------|------------------------------------------|  
    |Texto da consulta|Configure a consulta, incluindo a sua definição como expressão.|Não pode alterar a consulta.|  
    |Parâmetros de consulta|Não pode referenciar parâmetros de relatório<br /><br /> Inclui valores padrão<br /><br /> Inclui um sinalizador Somente Leitura|Configure parâmetros que não são marcados como Somente Leitura na definição|  
    |Filtros|Definir filtros|Não é possível exibir ou alterar filtros de conjuntos de dados que fazem parte da definição<br /><br /> Pode criar filtros adicionais|  
    |fonte de dados|Deve ser uma fonte de dados compartilhada|Não pode alterar a fonte de dados|  
    |Campos|Campos do comando query<br /><br /> Campos calculados não fazem parte da definição do conjunto de dados|Exiba os campos, mas não é possível alterá-los<br /><br /> A coleção de campos é estática com base na consulta no momento em que você adicionou o conjunto de dados compartilhado ao relatório. Para atualizar, clique em **Atualizar Campos** na caixa de diálogo **Propriedades do Conjunto de Dados** . A coleção de campos real é o que quer que seja retornado pela consulta atual na definição.<br /><br /> Adicionar campos calculados|  
    |Dataset|Opções de dados, como a diferenciação de maiúsculas e minúsculas|Substitua as opções de dados na instância|  
  
## <a name="embedded-datasets"></a>Conjuntos de dados inseridos  
 Use um conjunto de dados inserido quando você desejar obter dados de uma fonte de dados externa a ser usada somente em um relatório. Os conjuntos de dados inseridos são úteis quando você deseja criar uma consulta que não tem outras dependências e que não precisa ser usada para vários relatórios.  
  
 Para criar ou editar um conjunto de dados inserido, use o painel de dados do relatório. Após criar um conjunto de dados, você poderá configurar as propriedades na caixa de diálogo **Propriedades de Conjunto de Dados** .  
  
## <a name="see-also"></a>Consulte também  
 [Inseridos e compartilhados, conexões de dados ou fontes de dados &#40;relatórios e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
