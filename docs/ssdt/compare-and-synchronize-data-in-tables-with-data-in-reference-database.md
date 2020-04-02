---
title: Comparar e sincronizar dados em tabelas dentro de um banco de dados de referência
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 96d743b0-b69a-45bb-ae0e-62103dca76e2
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/27/2020
ms.openlocfilehash: 097a024622dd7550ec3dabac1c1fac2a35dfe4b3
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402620"
---
# <a name="compare-and-synchronize-data-in-one-or-more-tables-with-data-in-a-reference-database"></a>Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência

Você pode comparar os dados em um banco de dados de *origem* e em um banco de dados de *destino* e especificar quais tabelas devem ser comparadas. Os dados podem ser examinados para orientar uma decisão sobre quais alterações deverão ser sincronizadas. Em seguida, você atualizaria o destino para sincronizar os bancos de dados ou exportaria o script de atualização para o editor Transact\-SQL ou para um arquivo.  
  
Talvez você pudesse sincronizar bancos de dados para atualizar um servidor de preparo com uma cópia dos dados de produção. Você também pode sincronizar uma ou mais tabelas para populá-las com dados de referência de outro banco de dados. Além disso, você poderia comparar dados antes e depois de executar testes como uma forma adicional de verificação.  
  
Você pode comparar dados em dois bancos de dados, mas não pode especificar um arquivo de projeto de banco de dados ou um .dacpac para comparação porque ele não contém dados.  
  
Esta seção contém os seguintes tipos de informação:  
  
-   [Como: comparar e sincronizar os dados de dois bancos de dados](../ssdt/how-to-compare-and-synchronize-the-data-of-two-databases.md)  
  
-   [Como: exibir diferenças de dados](../ssdt/how-to-view-data-differences.md)  
  
## <a name="requirements"></a>Requisitos  
Quando você compara dados em uma tabela ou exibição, a tabela ou exibição no banco de dados de origem deve compartilhar vários atributos com uma tabela ou exibição no banco de dados de destino. Tabelas e exibições que não atendem aos seguintes critérios não são comparadas e não aparecem na segunda página do assistente **Nova Comparação de Dados**:  
  
-   As tabelas devem ter nomes de colunas correspondentes com tipos de dados compatíveis.  
  
    Os nomes de tabelas, exibições e proprietários diferenciam maiúsculas de minúsculas.  
  
-   As tabelas devem ter a mesma chave primária, índice exclusivo ou restrição exclusiva.  
  
-   As exibições devem ter o mesmo índices exclusivo e clusterizado.  
  
-   Você pode comparar uma tabela com uma exibição somente se elas tiverem o mesmo nome.  
  
Cada objeto tem uma chave ou índice que determina os outros objetos aos quais correspondem. Cada tabela ou exibição pode ter mais de uma chave primária, índice exclusivo ou restrição exclusiva. Sendo assim, convém especificar qual chave, índice ou restrição deve ser usado.  
  
## <a name="common-tasks"></a>Tarefas comuns  
Nesta seção, você pode encontrar descrições das tarefas comuns que oferecem suporte para esse cenário.  
  
**Definir opções para controlar como os dados são comparados:** quando você compara dados, pode ignorar as colunas de identidade, desabilitar gatilhos e desabilitar chaves estrangeiras. Você também pode ignorar chaves primárias, índices e restrições exclusivas do script de atualização.  
  
**Comparar dados em tabelas e, opcionalmente, atualizar o destino para corresponder à origem:** Depois de especificar uma origem e um banco de dados de destino com o qual comparar e executar a comparação, veja os resultados na janela **Comparação de Dados**. Veja não somente os detalhes das diferenças, mas também o script de atualização que é usado para sincronizar os dados. Depois de identificar as diferenças entre os dois bancos de dados, especifique uma ação para cada diferença. Em seguida, atualize o destino ou exportar o script de atualização para o editor Transact\-SQL ou para um arquivo. Talvez você queira exportar o script de modo que você ou outra pessoa possa examiná-lo antes de aplicar as alterações.  
  
## <a name="understanding-comparison-results"></a><a name="UnderstandingDataCompareResults"></a>Entender os resultados da comparação  
A tabela a seguir descreve as cinco colunas na janela **Comparação de Dados**.  
  
|Coluna|Observações|  
|----------|---------|  
|Objeto|Exibe o nome da tabela ou exibição e uma caixa de seleção que indica se o destino deve ser sincronizado quando você escreve atualizações ou exporta o script de atualização. A caixa de seleção não está disponível para as tabelas ou exibições que não contêm dados.|  
|Registros diferentes|Exibe o número de registros no destino que tem a mesma chave, mas não os mesmos dados que na origem. Os parênteses incluem o número de registros marcados para atualização você escreve atualizações ou exporta o script de atualização.|  
|Somente na Origem|Exibe o número de registros na origem que não ocorre no destino. Os parênteses incluem o número de registros marcados para adição quando você escreve atualizações ou exporta o script de atualização.|  
|Somente no Destino|Exibe o número de registros no destino que não ocorre na origem. Os parênteses incluem o número dos registros marcados para serem exclusão quando você escreve atualizações ou exporta o script de atualização.|  
|Registros idênticos|Exibe o número de registros no destino que tem a mesma chave e os mesmos dados que na origem. Esses registros não são atualizados quando você escreve atualizações ou exporta o script de atualização.|  
  
### <a name="table-and-view-details"></a>Detalhes de tabela e de exibição  
Quando você clica em qualquer tabela ou exibição na janela **Comparação de Dados**, o painel de detalhes exibe todas as linhas que a tabela ou exibição contém. Cada guia no painel de detalhes exibe uma categoria diferente (Registros Diferentes, Somente na Origem, Somente no Destino, Registros Idênticos). Para cada linha, marque ou desmarque a caixa de seleção correspondente para indicar se você deseja incluir essa alteração no script de atualização.  
  
## <a name="see-also"></a>Consulte Também  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
[Como: Usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
