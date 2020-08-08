---
title: Selecionando e configurando objetos afetados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 619da90c19cf918b3f53ac6cd213b27e718b6a10
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932907"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>Selecionar e configurar os objetos afetados (OracleToSQL)
Nesta página, você pode selecionar tabelas e chaves estrangeiras, alterações que devem ser comparadas quando o SSMA verifica os resultados da execução dos objetos escolhidos na etapa anterior. Além disso, você pode personalizar os parâmetros de verificação.  
  
## <a name="selection-of-affected-objects"></a>Seleção de objetos afetados  
Na árvore de objetos do Oracle, localizada no lado esquerdo da janela, verifique as tabelas e as chaves estrangeiras, as alterações que devem ser comparadas para serem idênticas.  
  
Se o SSMA Tester não puder verificar nenhum desses objetos, você verá que o link rotulado **alguns objetos selecionados contém erros** na árvore de objetos. Clique neste link para exibir os motivos pelos quais esses objetos não podem ser comparados e para limpar a seleção de objetos errados.  
  
## <a name="table"></a>Tabela  
A guia tabela contém a exibição de grade da tabela selecionada. A grade contém as seguintes informações sobre a tabela selecionada:  
  
-   Nome da coluna  
  
-   Tipo de Dados  
  
-   Precisão  
  
-   Escala  
  
-   Regra  
  
-   Padrão  
  
-   Identidade  
  
-   Nullable  
  
## <a name="sql"></a>Sql  
A guia SQL contém o SQL "criar tabela" da tabela selecionada.  
  
## <a name="data"></a>Dados  
Guia dados exibe os dados presentes na tabela selecionada.  
  
## <a name="properties"></a>Propriedades  
A guia Propriedades exibe as propriedades da tabela selecionada. Os campos a seguir estão presentes na guia Propriedades:  
  
-   Criado ou modificado pela última vez  
  
-   Nome do Objeto  
  
## <a name="columns-comparison-settings"></a>Configurações de comparação de colunas  
Estabelecer as regras de comparação para colunas de tabela na página de **comparação de colunas** . Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Usar durante comparações de teste  
Determine se esta coluna participará da verificação de resultados de teste.  
  
-   Se você escolher **true**, o SSMA comparará o conteúdo desta coluna depois de executar o teste no Oracle com o conteúdo da coluna em SQL Server. 
  
-   Se você escolher**false**, a coluna será excluída da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para colunas de tipo de dados numéricos, você pode definir uma escala personalizada para a comparação.  
  
-   Se você escolher **true**, os valores numéricos serão arredondados de acordo com o valor de **escala de comparação** antes de serem comparados.  
  
-   Se você escolher**false**, a comparação numérica será exata.  
  
### <a name="comparing-scale"></a>Comparando escala  
  
-   Disponível somente se a opção **usar escala personalizada** estiver definida como **true**. Essa é a precisão para comparação numérica.  
  
### <a name="date-time-comparing"></a>Comparação de data e hora  
Define como os valores de data/hora são comparados.  
  
-   Se você selecionar **comparar data inteira**, a comparação completa de valores de ambas as plataformas será executada.  
  
-   Se você selecionar **comparar somente data**, a parte de hora será ignorada.  
  
-   Se você selecionar **comparar apenas hora**, a parte de data será ignorada.  
  
-   Se você selecionar **ignorar milissegundos**, os resultados serão comparados a até segundos.  
  
-   Se você selecionar **ignorar data e milissegundos**, o resultado será comparado apenas por parte do tempo e ignorando partes fracionárias de um segundo.  
  
### <a name="ignore-strings-case"></a>Ignorar caso de cadeia de caracteres  
Controla a sensibilidade do caso de comparação.  
  
-   Se você escolher **true**, a comparação não diferenciará maiúsculas de minúsculas.  
  
-   Se você escolher **false**, a comparação considerará o caso de letra.  
  
## <a name="comparing-sql"></a>Comparando SQL  
Você pode exibir as instruções SELECT geradas pelo SSMA Tester na página **comparando SQL** . O testador irá comparar os conjuntos de resultados dessas instruções linha por linha. Cada linha seguinte de um conjunto de resultados Oracle deve ser igual à linha seguinte do conjunto de resultados produzido em SQL Server.
  
Você pode editar essas instruções SELECT para fornecer verificação personalizada. Para salvar as alterações no Oracle e em instruções SQL Server, use os botões **aplicar** sob o SQL de origem e de destino, de forma correspondente.  
  
## <a name="next-step"></a>Próxima etapa  
[Personalizando a ordem das chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Concluindo a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[Executando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
